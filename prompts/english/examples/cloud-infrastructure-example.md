# Example: Cloud Infrastructure with Terraform & Kubernetes

> Real-world walkthrough of deploying a production-ready infrastructure using the APEI cycle with **Agent System** + **Cloud & Infrastructure** prompts.

## Context

**Task**: Deploy a Node.js API with PostgreSQL database to AWS using Terraform and Kubernetes (EKS), with auto-scaling, monitoring, and zero-downtime deployments.

**Prompts Used**: `claude-agent-system-prompt.md` + `cloud-infrastructure-prompt.md`

---

## Iteration 1: Infrastructure Foundation

### ANALYZE

```markdown
## Assessment
- Application: Node.js REST API with PostgreSQL
- Scale: 1000-5000 concurrent users
- Requirements: Auto-scaling, zero-downtime deploys, multi-AZ
- Budget: $500-1500/month
- Compliance: SOC 2 (audit logs, encryption)
```

**Current state**: No infrastructure exists. Starting from scratch.

### PLAN

```markdown
## Infrastructure Plan
1. VPC with public/private subnets across 3 AZs
2. EKS cluster with managed node groups
3. RDS PostgreSQL (Multi-AZ) in private subnets
4. Application Load Balancer with TLS termination
5. ECR for container registry
6. Secrets Manager for database credentials
7. CloudWatch for logs and metrics
```

### EXECUTE

#### 1. VPC Module
```hcl
# modules/networking/main.tf
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "~> 5.0"

  name = "${var.project}-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["us-east-1a", "us-east-1b", "us-east-1c"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  public_subnets  = ["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]

  enable_nat_gateway   = true
  single_nat_gateway   = false  # One per AZ for high availability
  enable_dns_hostnames = true

  # Tags required for EKS
  public_subnet_tags = {
    "kubernetes.io/role/elb" = 1
  }
  private_subnet_tags = {
    "kubernetes.io/role/internal-elb" = 1
  }

  tags = var.common_tags
}
```

#### 2. EKS Cluster
```hcl
# modules/compute/eks.tf
module "eks" {
  source  = "terraform-aws-modules/eks/aws"
  version = "~> 20.0"

  cluster_name    = "${var.project}-cluster"
  cluster_version = "1.29"

  vpc_id     = var.vpc_id
  subnet_ids = var.private_subnet_ids

  # Enable IRSA for pod-level IAM
  enable_irsa = true

  cluster_endpoint_public_access = true
  cluster_endpoint_private_access = true

  eks_managed_node_groups = {
    general = {
      instance_types = ["t3.medium"]
      min_size       = 2
      max_size       = 8
      desired_size   = 3

      labels = { workload = "general" }
    }
  }

  # Cluster add-ons
  cluster_addons = {
    coredns    = { most_recent = true }
    kube-proxy = { most_recent = true }
    vpc-cni    = { most_recent = true }
  }

  tags = var.common_tags
}
```

#### 3. RDS PostgreSQL
```hcl
# modules/database/rds.tf
module "rds" {
  source  = "terraform-aws-modules/rds/aws"
  version = "~> 6.0"

  identifier = "${var.project}-postgres"

  engine               = "postgres"
  engine_version       = "16.1"
  family               = "postgres16"
  major_engine_version = "16"
  instance_class       = "db.t3.medium"
  allocated_storage    = 50

  db_name  = var.db_name
  username = var.db_username
  port     = 5432

  multi_az               = true
  db_subnet_group_name   = aws_db_subnet_group.this.name
  vpc_security_group_ids = [aws_security_group.rds.id]

  backup_retention_period = 30
  backup_window          = "03:00-04:00"
  maintenance_window     = "Mon:04:00-Mon:05:00"

  performance_insights_enabled = true
  monitoring_interval         = 60
  monitoring_role_arn         = aws_iam_role.rds_monitoring.arn

  deletion_protection = true
  storage_encrypted   = true

  tags = var.common_tags
}

# Store credentials in Secrets Manager
resource "aws_secretsmanager_secret" "db_credentials" {
  name = "${var.project}/db-credentials"
}

resource "aws_secretsmanager_secret_version" "db_credentials" {
  secret_id = aws_secretsmanager_secret.db_credentials.id
  secret_string = jsonencode({
    username = module.rds.db_instance_username
    password = random_password.db.result
    host     = module.rds.db_instance_address
    port     = module.rds.db_instance_port
    dbname   = var.db_name
  })
}
```

#### 4. Kubernetes Manifests
```yaml
# k8s/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-server
  namespace: production
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: api-server
  template:
    metadata:
      labels:
        app: api-server
    spec:
      serviceAccountName: api-server
      containers:
      - name: api
        image: 123456789.dkr.ecr.us-east-1.amazonaws.com/api-server:v1.0.0
        ports:
        - containerPort: 3000
        env:
        - name: NODE_ENV
          value: "production"
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: db-credentials
              key: url
        resources:
          requests:
            cpu: 250m
            memory: 256Mi
          limits:
            cpu: 500m
            memory: 512Mi
        livenessProbe:
          httpGet:
            path: /health/live
            port: 3000
          initialDelaySeconds: 15
          periodSeconds: 20
        readinessProbe:
          httpGet:
            path: /health/ready
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 10
      topologySpreadConstraints:
      - maxSkew: 1
        topologyKey: topology.kubernetes.io/zone
        whenUnsatisfied: DoNotSchedule
        labelSelector:
          matchLabels:
            app: api-server
---
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: api-server-hpa
  namespace: production
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: api-server
  minReplicas: 3
  maxReplicas: 20
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 60
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 75
```

### ITERATE

```
✅ VPC deployed with 3 AZs
✅ EKS cluster running with managed nodes
✅ RDS Multi-AZ with encryption and backups
✅ API deployed with 3 replicas
✅ HPA configured for auto-scaling

⚠️ Issues Found:
1. No ingress controller — need ALB Ingress
2. No TLS termination — need cert-manager
3. No monitoring — need CloudWatch + Prometheus
```

---

## Iteration 2: Production Hardening

### ANALYZE

Missing: TLS, monitoring, CI/CD pipeline, cost alerting

### EXECUTE

#### 5. ALB Ingress + TLS
```yaml
# k8s/ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: api-ingress
  namespace: production
  annotations:
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/target-type: ip
    alb.ingress.kubernetes.io/certificate-arn: arn:aws:acm:us-east-1:123456:certificate/xxx
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTPS":443}]'
    alb.ingress.kubernetes.io/ssl-redirect: "443"
    alb.ingress.kubernetes.io/healthcheck-path: /health/ready
spec:
  ingressClassName: alb
  rules:
  - host: api.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: api-server
            port:
              number: 3000
```

#### 6. CI/CD Pipeline
```yaml
# .github/workflows/deploy.yml
name: Build & Deploy
on:
  push:
    branches: [main]

env:
  AWS_REGION: us-east-1
  ECR_REPOSITORY: api-server
  EKS_CLUSTER: myproject-cluster

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci && npm test
      - run: npm run lint

  build-and-push:
    needs: test
    runs-on: ubuntu-latest
    outputs:
      image-tag: ${{ steps.build.outputs.image-tag }}
    steps:
      - uses: actions/checkout@v4
      - uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: ${{ secrets.AWS_ROLE_ARN }}
          aws-region: ${{ env.AWS_REGION }}
      - uses: aws-actions/amazon-ecr-login@v2
        id: ecr
      - name: Build and push
        id: build
        run: |
          IMAGE_TAG=${{ github.sha }}
          docker build -t ${{ steps.ecr.outputs.registry }}/$ECR_REPOSITORY:$IMAGE_TAG .
          docker push ${{ steps.ecr.outputs.registry }}/$ECR_REPOSITORY:$IMAGE_TAG
          echo "image-tag=$IMAGE_TAG" >> $GITHUB_OUTPUT

  deploy:
    needs: build-and-push
    runs-on: ubuntu-latest
    environment: production
    steps:
      - uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: ${{ secrets.AWS_ROLE_ARN }}
          aws-region: ${{ env.AWS_REGION }}
      - run: aws eks update-kubeconfig --name $EKS_CLUSTER
      - run: |
          kubectl set image deployment/api-server \
            api=${{ needs.build-and-push.outputs.image-tag }} \
            -n production
          kubectl rollout status deployment/api-server -n production --timeout=300s
```

#### 7. Monitoring
```hcl
# modules/monitoring/cloudwatch.tf
resource "aws_cloudwatch_metric_alarm" "cpu_high" {
  alarm_name          = "${var.project}-cpu-high"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 2
  metric_name         = "CPUUtilization"
  namespace           = "AWS/ECS"
  period              = 300
  statistic           = "Average"
  threshold           = 80
  alarm_actions       = [aws_sns_topic.alerts.arn]
}

resource "aws_cloudwatch_metric_alarm" "error_rate" {
  alarm_name          = "${var.project}-error-rate"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 2
  metric_name         = "5XXError"
  namespace           = "AWS/ApplicationELB"
  period              = 300
  statistic           = "Sum"
  threshold           = 50
  alarm_actions       = [aws_sns_topic.alerts.arn]
}
```

### Final Results

```
✅ Infrastructure deployed with Terraform
✅ EKS cluster with auto-scaling (3-20 pods)
✅ RDS PostgreSQL Multi-AZ with 30-day backups
✅ TLS termination via ALB + ACM
✅ CI/CD pipeline: test → build → deploy
✅ Monitoring with CloudWatch alarms
✅ Cost alerting at 80% and 100% budget

📊 Metrics:
- Deployment time: ~3 minutes (zero-downtime)
- Infrastructure provisioning: ~15 minutes
- Monthly cost estimate: $800-1200
- Availability target: 99.95%
- RPO: 0 (Multi-AZ), RTO: < 15 min
```
