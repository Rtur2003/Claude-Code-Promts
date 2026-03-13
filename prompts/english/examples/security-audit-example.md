# Example: Security Audit of a Node.js API

## Scenario

You are tasked with performing a security audit on an existing Node.js/Express API that handles user data and payment processing. The application has been in production for 6 months with no prior security review.

## Prompts Used

1. **Agent System Prompt** - APEI workflow
2. **Security Audit Prompt** - Vulnerability detection and remediation

---

## Phase 1: Reconnaissance

### Step 1: ANALYZE

```markdown
## Audit Scope

**Application**: Payment processing REST API
**Stack**: Node.js 18, Express 4, MongoDB, Stripe SDK
**Endpoints**: 23 routes across 5 routers
**Authentication**: JWT with custom implementation
**Data Sensitivity**: PII (names, emails), payment tokens

### Attack Surface
- Public endpoints: 4 (login, register, health, webhook)
- Authenticated endpoints: 19
- Admin endpoints: 6
- File upload endpoints: 1
- Third-party integrations: Stripe, SendGrid
```

### Dependency Scan

```bash
npm audit
```

```
# Results
found 12 vulnerabilities (3 critical, 4 high, 5 moderate)

┌──────────────┬────────────────────────────────────────┐
│ Critical     │ jsonwebtoken < 9.0.0                   │
│              │ JWT verification bypass via algorithm   │
│              │ confusion attack                        │
├──────────────┼────────────────────────────────────────┤
│ Critical     │ mongoose < 7.0.0                       │
│              │ Prototype pollution in query parsing    │
├──────────────┼────────────────────────────────────────┤
│ Critical     │ multer < 1.4.5                         │
│              │ Path traversal in file uploads          │
├──────────────┼────────────────────────────────────────┤
│ High         │ express-session < 1.18.0               │
│              │ Session fixation vulnerability          │
└──────────────┴────────────────────────────────────────┘
```

### Endpoint Analysis

```markdown
### High-Risk Endpoints
1. POST /api/auth/login         - No rate limiting
2. POST /api/payments/charge    - Direct card data handling
3. PUT  /api/users/:id          - No ownership validation
4. POST /api/uploads/avatar     - No file type validation
5. GET  /api/admin/users        - Role check in route only
```

---

## Phase 2: Vulnerability Assessment

### Finding 1: SQL/NoSQL Injection

```javascript
// VULNERABLE: src/controllers/userController.js
const searchUsers = async (req, res) => {
    const { name, role } = req.query;

    // User input directly in query — NoSQL injection possible
    const users = await User.find({
        name: { $regex: name },
        role: role,
    });

    res.json(users);
};
```

**Attack Vector**:
```bash
# NoSQL injection via query parameter
GET /api/users/search?role[$ne]=null
# Returns ALL users regardless of role
```

**Severity**: 🔴 Critical

---

### Finding 2: Broken Authentication

```javascript
// VULNERABLE: src/middleware/auth.js
const jwt = require('jsonwebtoken');

const authenticate = (req, res, next) => {
    const token = req.headers.authorization?.split(' ')[1];

    // Algorithm not specified — allows "none" algorithm attack
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
};
```

**Attack Vector**:
```javascript
// Attacker crafts a token with "none" algorithm
const header = Buffer.from('{"alg":"none","typ":"JWT"}').toString('base64url');
const payload = Buffer.from('{"userId":"admin-id","role":"admin"}').toString('base64url');
const maliciousToken = `${header}.${payload}.`;
```

**Severity**: 🔴 Critical

---

### Finding 3: Insecure Direct Object Reference (IDOR)

```javascript
// VULNERABLE: src/controllers/userController.js
const updateUser = async (req, res) => {
    // Any authenticated user can update ANY user's profile
    const user = await User.findByIdAndUpdate(
        req.params.id,  // No ownership check!
        req.body,
        { new: true }
    );

    res.json(user);
};
```

**Attack Vector**:
```bash
# Authenticated as user-A, updating user-B's data
PUT /api/users/user-b-id
Authorization: Bearer <user-a-token>
{"name": "Hacked", "role": "admin"}
```

**Severity**: 🔴 Critical

---

### Finding 4: Cross-Site Scripting (XSS)

```javascript
// VULNERABLE: src/controllers/commentController.js
const createComment = async (req, res) => {
    // Stored XSS — no sanitization on input
    const comment = await Comment.create({
        body: req.body.content,  // Raw HTML stored
        userId: req.user.id,
    });

    res.status(201).json(comment);
};

// Later rendered without escaping in email templates
const html = `<p>New comment: ${comment.body}</p>`;
```

**Severity**: 🟠 High

---

### Finding 5: Missing Rate Limiting

```javascript
// VULNERABLE: src/routes/auth.js
router.post('/login', authController.login);
router.post('/register', authController.register);
router.post('/forgot-password', authController.forgotPassword);
// No rate limiting on any auth endpoint
```

**Severity**: 🟠 High

---

### Finding 6: Sensitive Data Exposure

```javascript
// VULNERABLE: src/controllers/userController.js
const getUser = async (req, res) => {
    const user = await User.findById(req.params.id);
    // Returns password hash, tokens, and internal fields
    res.json(user);
};
```

**Severity**: 🟡 Medium

---

## Phase 3: Findings Summary

```markdown
## Security Audit Report

### Summary
| Severity | Count | Status     |
|----------|-------|------------|
| Critical | 3     | Must fix   |
| High     | 2     | Must fix   |
| Medium   | 4     | Should fix |
| Low      | 3     | Can defer  |

### Critical Findings
1. NoSQL injection in user search endpoint
2. JWT algorithm confusion vulnerability
3. IDOR on user update endpoint

### High Findings
4. Stored XSS in comment system
5. Missing rate limiting on authentication endpoints

### Medium Findings
6. Sensitive data exposure in user API responses
7. Missing CORS configuration
8. No request body size limits
9. Verbose error messages in production

### Low Findings
10. Missing security headers (X-Frame-Options, CSP)
11. No request ID tracking for audit trail
12. Session tokens in URL parameters on password reset
```

---

## Phase 4: Remediation

### Fix 1: NoSQL Injection → Input Sanitization

```javascript
// BEFORE (vulnerable)
const users = await User.find({
    name: { $regex: name },
    role: role,
});

// AFTER (secure)
const sanitize = require('mongo-sanitize');

const searchUsers = async (req, res) => {
    const name = sanitize(req.query.name);
    const role = sanitize(req.query.role);

    const allowedRoles = ['user', 'editor'];
    if (role && !allowedRoles.includes(role)) {
        return res.status(400).json({ error: 'Invalid role filter' });
    }

    const users = await User.find({
        name: { $regex: new RegExp(escapeRegex(name), 'i') },
        ...(role && { role }),
    }).select('-password -__v');

    res.json(users);
};

function escapeRegex(str) {
    return str.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
}
```

### Fix 2: JWT Algorithm Confusion → Explicit Algorithm

```javascript
// BEFORE (vulnerable)
const decoded = jwt.verify(token, process.env.JWT_SECRET);

// AFTER (secure)
const authenticate = (req, res, next) => {
    try {
        const token = req.headers.authorization?.split(' ')[1];

        if (!token) {
            return res.status(401).json({ error: 'Token required' });
        }

        const decoded = jwt.verify(token, process.env.JWT_SECRET, {
            algorithms: ['HS256'],  // Explicitly allow only HS256
            maxAge: '1h',
            issuer: 'payment-api',
        });

        req.user = decoded;
        next();
    } catch (error) {
        return res.status(401).json({ error: 'Invalid token' });
    }
};
```

### Fix 3: IDOR → Ownership Validation

```javascript
// BEFORE (vulnerable)
const user = await User.findByIdAndUpdate(req.params.id, req.body, { new: true });

// AFTER (secure)
const updateUser = async (req, res) => {
    if (req.user.userId !== req.params.id && req.user.role !== 'admin') {
        return res.status(403).json({ error: 'Not authorized' });
    }

    const allowedFields = ['name', 'email', 'avatar'];
    const updates = Object.keys(req.body)
        .filter((key) => allowedFields.includes(key))
        .reduce((obj, key) => ({ ...obj, [key]: req.body[key] }), {});

    const user = await User.findByIdAndUpdate(
        req.params.id,
        updates,
        { new: true, runValidators: true }
    ).select('-password -__v');

    if (!user) {
        return res.status(404).json({ error: 'User not found' });
    }

    res.json(user);
};
```

### Fix 4: XSS → Input Sanitization

```javascript
// BEFORE (vulnerable)
const comment = await Comment.create({
    body: req.body.content,
    userId: req.user.id,
});

// AFTER (secure)
const createDOMPurify = require('dompurify');
const { JSDOM } = require('jsdom');
const DOMPurify = createDOMPurify(new JSDOM('').window);

const createComment = async (req, res) => {
    const sanitizedContent = DOMPurify.sanitize(req.body.content, {
        ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'p'],
        ALLOWED_ATTR: [],
    });

    const comment = await Comment.create({
        body: sanitizedContent,
        userId: req.user.id,
    });

    res.status(201).json(comment);
};
```

### Fix 5: Rate Limiting → Express Rate Limit

```javascript
// BEFORE (vulnerable)
router.post('/login', authController.login);

// AFTER (secure)
const rateLimit = require('express-rate-limit');

const authLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,  // 15 minutes
    max: 5,                     // 5 attempts per window
    message: { error: 'Too many attempts, please try again later' },
    standardHeaders: true,
    legacyHeaders: false,
});

router.post('/login', authLimiter, authController.login);
router.post('/register', authLimiter, authController.register);
router.post('/forgot-password', authLimiter, authController.forgotPassword);
```

---

## Final Security Report

```markdown
## Security Audit Report — Payment API

**Date**: 2024-01-15
**Auditor**: AI Security Agent
**Scope**: Full application audit (code, dependencies, configuration)

### Executive Summary
The application contained 12 vulnerabilities including 3 critical findings
that could allow unauthorized data access and privilege escalation.
All critical and high severity issues have been remediated.

### Remediation Status
| # | Finding                    | Severity | Status |
|---|----------------------------|----------|--------|
| 1 | NoSQL injection            | Critical | ✅ Fixed |
| 2 | JWT algorithm confusion    | Critical | ✅ Fixed |
| 3 | IDOR on user update        | Critical | ✅ Fixed |
| 4 | Stored XSS                 | High     | ✅ Fixed |
| 5 | Missing rate limiting      | High     | ✅ Fixed |
| 6 | Sensitive data exposure    | Medium   | ✅ Fixed |
| 7 | Missing CORS config        | Medium   | ✅ Fixed |
| 8 | No body size limits        | Medium   | ✅ Fixed |
| 9 | Verbose error messages     | Medium   | ✅ Fixed |
| 10| Missing security headers   | Low      | ✅ Fixed |
| 11| No request ID tracking     | Low      | Deferred |
| 12| Tokens in URL params       | Low      | ✅ Fixed |

### Recommendations
1. Schedule quarterly dependency audits
2. Add automated security scanning to CI/CD pipeline
3. Implement request logging with audit trail
4. Conduct penetration testing before next major release

### Files Changed
- src/middleware/auth.js
- src/controllers/userController.js
- src/controllers/commentController.js
- src/routes/auth.js
- src/app.js (security headers, CORS, body limits)
- package.json (dependency updates)
```

### Commit
```
security(audit): remediate critical and high vulnerabilities

Fix 12 security vulnerabilities found during audit:
- Patch NoSQL injection in user search
- Enforce JWT algorithm to prevent confusion attacks
- Add ownership validation to prevent IDOR
- Sanitize HTML input to prevent stored XSS
- Add rate limiting on authentication endpoints
- Strip sensitive fields from API responses
- Update vulnerable dependencies

Closes #89
```

---

## Key Learnings

1. **Never trust user input** - Sanitize, validate, and whitelist at every boundary
2. **Be explicit with JWT** - Always specify allowed algorithms and set expiry
3. **Ownership checks are mandatory** - Authentication is not authorization
4. **Dependency audits save you** - Known CVEs are the easiest attack vector

## Related Prompts

- [Security Audit Prompt](../agents/security-audit-prompt.md)
- [Agent System Prompt](../agents/claude-agent-system-prompt.md)
- [API Development Prompt](../project-types/api-development-prompt.md)
