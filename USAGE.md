# Usage Guide

This guide provides detailed instructions and examples for using Claude Code Prompts effectively.

## Table of Contents
1. [Getting Started](#getting-started)
2. [Choosing the Right Prompt](#choosing-the-right-prompt)
3. [How to Use Prompts](#how-to-use-prompts)
4. [Complete Examples](#complete-examples)
5. [Advanced Usage](#advanced-usage)
6. [Troubleshooting](#troubleshooting)

## Getting Started

### Step 1: Understand Your Project

Before selecting a prompt, identify:
- **Project Type**: Web, API, data science, etc.
- **Current Stage**: New project, adding features, refactoring, bug fixing
- **Goals**: What do you want to achieve?
- **Constraints**: Time, resources, technical limitations

### Step 2: Select Appropriate Prompts

Choose one or more prompts based on your project:

| Project Type | Recommended Prompts |
|-------------|---------------------|
| React/Vue Web App | Foundation + Web Development |
| REST API | Foundation + API Development |
| ML Project | Foundation + Data Science & ML |
| Full Stack | Foundation + Web + API |
| General Development | Foundation only |

### Step 3: Provide Context to Claude

Start your session with:
```
I'm working on [PROJECT DESCRIPTION].

Please use the following system prompt:
[PASTE PROMPT CONTENT]

Let's begin by analyzing the current state of the project.
```

## Choosing the Right Prompt

### Foundation Prompt
**Use when:**
- Starting any new project
- Need general best practices
- Working on diverse tasks
- Want universal quality standards

**Provides:**
- Iterative development cycle
- Commit standards
- Error analysis methodology
- General code quality principles

### Web Development Prompt
**Use when:**
- Building user interfaces
- Working with React, Vue, Angular
- Dealing with responsive design
- Focusing on accessibility
- Optimizing frontend performance

**Adds to Foundation:**
- Component architecture patterns
- CSS/styling best practices
- Browser compatibility handling
- Core Web Vitals optimization
- Accessibility standards

### API Development Prompt
**Use when:**
- Building REST or GraphQL APIs
- Creating backend services
- Implementing authentication
- Designing data models
- Working with databases

**Adds to Foundation:**
- RESTful design principles
- HTTP status code guidelines
- Authentication patterns
- Database optimization
- API security measures

### Data Science & ML Prompt
**Use when:**
- Building ML models
- Analyzing data
- Creating data pipelines
- Training and evaluating models
- Deploying ML systems

**Adds to Foundation:**
- Data quality assessment
- EDA workflows
- Feature engineering
- Model development pipeline
- Experiment tracking

## How to Use Prompts

### Method 1: Direct Copy-Paste

1. Open the prompt file you need
2. Copy the entire content
3. Paste at the start of your Claude session
4. Begin your work

**Example:**
```
Please use this system prompt for our session:

[Full content of claude-foundation-prompt.md]

Now, I need to add user authentication to my Node.js API.
```

### Method 2: Reference by Link

If sharing context externally:
```
Please review and internalize the system prompt at:
prompts/english/base/claude-foundation-prompt.md

Then help me implement the feature described below...
```

### Method 3: Combining Prompts

For complex projects:
```
Please use the following prompts as your system context:

1. Foundation Prompt: [paste content]
2. Web Development Prompt: [paste content]

I'm building a React dashboard with real-time data.
```

## Complete Examples

### Example 1: Building a User Authentication System

#### Scenario
Building JWT authentication for a Node.js Express API

#### Setup
```
I'm building JWT-based authentication for my Express API.

System Prompt: [Use API Development Prompt]

Current state:
- Express server running on port 3000
- PostgreSQL database set up
- User model exists
- No authentication yet

Requirements:
- Login endpoint with email/password
- JWT token generation
- Protected routes
- Token refresh mechanism
```

#### Claude's Iterative Approach

**Iteration 1: Basic Authentication**

**Analyze:**
```
Current State Analysis:
- Express server operational
- Database schema present
- Dependencies: Need jsonwebtoken, bcrypt
- Risk: Need to secure password storage
- Success criteria: Users can log in and access protected routes
```

**Plan:**
```
Implementation Plan:
1. Install dependencies (jsonwebtoken, bcrypt)
2. Create password hashing utility
3. Create login endpoint
4. Create JWT generation utility
5. Create authentication middleware
6. Protect existing routes
7. Add tests
```

**Execute:**
```bash
# Step 1: Install dependencies
npm install jsonwebtoken bcrypt

# Step 2-6: Implement each component
# [Claude implements each step with tests]

# Step 7: Validate
npm test
```

**Evaluate:**
```
Results:
✓ Login works
✓ Tokens generated correctly
✓ Protected routes secure
✓ Tests pass (85% coverage)

Issues found:
⚠ Token expiration too short (1 hour)
⚠ No token refresh mechanism
⚠ Performance: bcrypt rounds could be optimized

Decision: Iterate to address issues
```

**Iteration 2: Token Refresh & Optimization**

**Analyze:**
```
Focus Areas:
1. Add refresh token mechanism
2. Optimize bcrypt performance
3. Extend access token lifetime strategically
```

**Plan:**
```
1. Implement refresh tokens (long-lived)
2. Store refresh tokens in database
3. Create refresh endpoint
4. Optimize bcrypt work factor
5. Update tests
```

**Execute & Evaluate:**
```
Results:
✓ Refresh tokens implemented
✓ Security maintained
✓ Performance improved (login 40% faster)
✓ Token lifetime balanced (15 min access, 7 day refresh)
✓ All tests pass (92% coverage)

Decision: Optimal solution achieved
```

### Example 2: Building a React Component

#### Scenario
Creating a reusable DataTable component

#### Setup
```
Building a reusable DataTable component for our React app.

System Prompt: [Use Web Development Prompt]

Requirements:
- Display tabular data
- Sortable columns
- Pagination
- Responsive
- Accessible
- TypeScript
```

#### Claude's Iterative Approach

**Iteration 1: Basic Structure**

**Analyze:**
```
Project Analysis:
- React 18 with TypeScript
- Tailwind CSS for styling
- React Testing Library for tests
- Need to maintain existing design patterns
```

**Plan:**
```
1. Create basic DataTable component structure
2. Implement data rendering
3. Add PropTypes/TypeScript types
4. Style with Tailwind
5. Add basic tests
```

**Execute:**
```typescript
// DataTable.tsx - Basic implementation
interface DataTableProps {
  data: any[];
  columns: Column[];
}

const DataTable: React.FC<DataTableProps> = ({ data, columns }) => {
  return (
    <table className="w-full">
      <thead>
        <tr>
          {columns.map(col => (
            <th key={col.key}>{col.label}</th>
          ))}
        </tr>
      </thead>
      <tbody>
        {data.map((row, idx) => (
          <tr key={idx}>
            {columns.map(col => (
              <td key={col.key}>{row[col.key]}</td>
            ))}
          </tr>
        ))}
      </tbody>
    </table>
  );
};
```

**Evaluate:**
```
Results:
✓ Component renders data
✓ TypeScript types correct
✓ Tests pass

Missing features:
- Sorting
- Pagination
- Accessibility
- Responsive design

Decision: Iterate to add features
```

**Iteration 2: Add Sorting & Pagination**

**Plan & Execute:**
```typescript
const DataTable: React.FC<DataTableProps> = ({ 
  data, 
  columns,
  pageSize = 10 
}) => {
  const [sortConfig, setSortConfig] = useState(null);
  const [currentPage, setCurrentPage] = useState(1);
  
  // Sorting logic
  const sortedData = useMemo(() => {
    if (!sortConfig) return data;
    
    return [...data].sort((a, b) => {
      if (a[sortConfig.key] < b[sortConfig.key]) {
        return sortConfig.direction === 'asc' ? -1 : 1;
      }
      if (a[sortConfig.key] > b[sortConfig.key]) {
        return sortConfig.direction === 'asc' ? 1 : -1;
      }
      return 0;
    });
  }, [data, sortConfig]);
  
  // Pagination logic
  const paginatedData = useMemo(() => {
    const start = (currentPage - 1) * pageSize;
    return sortedData.slice(start, start + pageSize);
  }, [sortedData, currentPage, pageSize]);
  
  // Render with sorting and pagination
  // ...
};
```

**Evaluate:**
```
Results:
✓ Sorting works
✓ Pagination works
✓ Performance good (useMemo)
✓ Tests updated and passing

Still missing:
- Accessibility (keyboard nav, ARIA)
- Mobile responsive design

Decision: Iterate for accessibility & responsiveness
```

**Iteration 3: Accessibility & Responsive**

**Execute:**
```typescript
const DataTable: React.FC<DataTableProps> = (props) => {
  // ... previous logic ...
  
  return (
    <div className="overflow-x-auto">
      <table 
        className="w-full min-w-full divide-y divide-gray-200"
        role="table"
        aria-label="Data table"
      >
        <thead className="bg-gray-50">
          <tr role="row">
            {columns.map(col => (
              <th
                key={col.key}
                scope="col"
                role="columnheader"
                tabIndex={0}
                onClick={() => handleSort(col.key)}
                onKeyPress={(e) => e.key === 'Enter' && handleSort(col.key)}
                className="px-6 py-3 text-left text-xs font-medium 
                           text-gray-500 uppercase tracking-wider cursor-pointer
                           hover:bg-gray-100 focus:outline-none focus:ring-2 
                           focus:ring-blue-500"
                aria-sort={getSortDirection(col.key)}
              >
                {col.label}
                <span aria-hidden="true">
                  {renderSortIcon(col.key)}
                </span>
              </th>
            ))}
          </tr>
        </thead>
        {/* ... tbody with proper ARIA attributes ... */}
      </table>
      
      {/* Responsive pagination */}
      <nav 
        className="flex items-center justify-between px-4 py-3 
                   sm:px-6 border-t"
        aria-label="Pagination"
      >
        {/* Pagination controls with ARIA */}
      </nav>
    </div>
  );
};
```

**Evaluate:**
```
Final Results:
✓ Fully accessible (WCAG AA)
✓ Keyboard navigation works
✓ Screen reader compatible
✓ Responsive on all devices
✓ All tests pass (95% coverage)
✓ Lighthouse accessibility score: 100

Decision: Optimal solution achieved
```

### Example 3: ML Model Development

#### Scenario
Customer churn prediction model

#### Setup
```
Building a customer churn prediction model.

System Prompt: [Use Data Science & ML Prompt]

Dataset: customer_data.csv
- 10,000 customers
- 20 features
- Target: churn (binary: 0/1)
- Class imbalance: 70% not churned, 30% churned

Goal: Predict customer churn with >85% accuracy
```

#### Claude's Iterative Approach

**Iteration 1: Baseline Model**

**Analyze:**
```python
# Data quality assessment
import pandas as pd

df = pd.read_csv('customer_data.csv')
print(f"Shape: {df.shape}")
print(f"Missing values: {df.isnull().sum().sum()}")
print(f"Class distribution: {df['churn'].value_counts()}")

# Results:
# - Shape: (10000, 21)
# - Missing values: 350 (3.5%)
# - Class imbalance confirmed
```

**Plan:**
```
1. Data cleaning and preprocessing
2. Exploratory data analysis
3. Feature engineering
4. Train baseline model (Logistic Regression)
5. Evaluate performance
6. Identify improvements
```

**Execute:**
```python
# Data preprocessing
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report, roc_auc_score

# Handle missing values
df = df.fillna(df.median())

# Split data
X = df.drop('churn', axis=1)
y = df['churn']
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# Scale features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train baseline
model = LogisticRegression(random_state=42)
model.fit(X_train_scaled, y_train)

# Evaluate
y_pred = model.predict(X_test_scaled)
print(classification_report(y_test, y_pred))
print(f"ROC AUC: {roc_auc_score(y_test, y_pred):.4f}")
```

**Evaluate:**
```
Results:
- Accuracy: 78%
- Precision: 72%
- Recall: 65%
- F1: 68%
- ROC AUC: 0.76

Issues:
- Below target accuracy (85%)
- Class imbalance not addressed
- Simple features (no engineering)

Decision: Iterate with better approach
```

**Iteration 2: Advanced Model with Feature Engineering**

**Plan:**
```
1. Address class imbalance (SMOTE or class weights)
2. Feature engineering
3. Try Random Forest (handles non-linearity)
4. Hyperparameter tuning
5. Cross-validation
```

**Execute:**
```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import GridSearchCV
from imblearn.over_sampling import SMOTE

# Feature engineering
df['tenure_age_ratio'] = df['tenure'] / (df['age'] + 1)
df['avg_monthly_spend'] = df['total_spend'] / (df['tenure'] + 1)
# ... more features

# Address class imbalance
smote = SMOTE(random_state=42)
X_train_balanced, y_train_balanced = smote.fit_resample(
    X_train_scaled, y_train
)

# Train Random Forest with tuning
param_grid = {
    'n_estimators': [100, 200],
    'max_depth': [10, 20, None],
    'min_samples_split': [2, 5],
}

rf = RandomForestClassifier(random_state=42)
grid_search = GridSearchCV(
    rf, param_grid, cv=5, scoring='roc_auc', n_jobs=-1
)
grid_search.fit(X_train_balanced, y_train_balanced)

best_model = grid_search.best_estimator_
```

**Evaluate:**
```
Results:
- Accuracy: 87%
- Precision: 84%
- Recall: 82%
- F1: 83%
- ROC AUC: 0.89
- CV Score: 0.86 (+/- 0.02)

✓ Exceeds target accuracy
✓ Balanced precision/recall
✓ No overfitting
✓ Stable cross-validation

Decision: Optimal solution achieved
```

## Advanced Usage

### Combining Multiple Prompts

For full-stack applications:
```
System Context:
1. Foundation Prompt: [core principles]
2. Web Development Prompt: [frontend guidelines]
3. API Development Prompt: [backend guidelines]

Project: E-commerce platform
Frontend: React
Backend: Node.js Express
Database: PostgreSQL
```

### Customizing for Your Team

Add team-specific standards:
```
[Include Foundation Prompt]

## Additional Team Standards

### Our Tech Stack
- Frontend: Next.js 14 with TypeScript
- Backend: NestJS
- Database: PostgreSQL with Prisma
- Testing: Jest + Playwright

### Our Conventions
- Use conventional commits
- Minimum 80% test coverage
- All PRs require 2 approvals
- Follow our internal style guide at docs/style-guide.md
```

## Troubleshooting

### Issue: Claude not following the prompt

**Solution:** Reinforce the prompt:
```
Remember to follow the system prompt provided earlier.
Specifically:
- Analyze before planning
- Make minimal changes
- Test after each step
```

### Issue: Too many iterations

**Solution:** Set clear completion criteria:
```
Let's iterate until we achieve:
- All tests passing
- Performance target met (<200ms response time)
- No security vulnerabilities

Maximum 3 iterations.
```

### Issue: Scope creep during iteration

**Solution:** Reset focus:
```
Let's refocus on the original goal:
[Original goal]

Current iteration should only address:
[Specific issue]

Other improvements can be future iterations.
```

## Tips for Success

1. **Be Specific**: Provide clear requirements and constraints
2. **Trust the Process**: Let Claude follow the Analyze-Plan-Execute-Iterate cycle
3. **Validate Often**: Test after each meaningful change
4. **Know When to Stop**: Perfect is the enemy of good enough
5. **Document Learnings**: Keep notes on what works for your projects

## Next Steps

- Review the [Iterative Development Guide](../prompts/english/workflows/iterative-development-guide.md)
- Check out examples in the prompts directory
- Customize prompts for your specific needs
- Share feedback and improvements

---

**Remember**: These prompts are tools to enhance development. Adapt them to your workflow and continuously improve based on results.
