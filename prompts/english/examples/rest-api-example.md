# Example: Building a REST API

## Scenario

You need to build a user management REST API with Node.js and Express, including:
- CRUD operations for users
- JWT authentication
- Input validation
- Error handling

## Prompts Used

1. **Foundation Prompt** - Core development principles
2. **API Development Prompt** - REST API best practices
3. **Agent System Prompt** - APEI workflow

---

## Step 1: ANALYZE

### Initial Analysis
```markdown
## Analysis Summary

**Problem**: Build a user management REST API with authentication
**Stack**: Node.js, Express, PostgreSQL, JWT
**Key Files**: 
- src/routes/users.js
- src/controllers/userController.js
- src/middleware/auth.js
- src/models/User.js
**Risks**: 
- SQL injection if not using parameterized queries
- JWT secret exposure
- Password storage security
**Success Criteria**: 
- All CRUD endpoints working
- JWT authentication implemented
- Input validation on all endpoints
- 80%+ test coverage
```

### Project Structure Analysis
```
src/
├── config/
│   └── database.js
├── controllers/
│   └── userController.js
├── middleware/
│   ├── auth.js
│   ├── validate.js
│   └── errorHandler.js
├── models/
│   └── User.js
├── routes/
│   └── users.js
├── utils/
│   └── jwt.js
└── app.js
```

---

## Step 2: PLAN

### Implementation Plan

#### Phase 1: Foundation (Day 1)
- [ ] Set up Express application
- [ ] Configure PostgreSQL connection
- [ ] Set up project structure
- [ ] Configure ESLint and Prettier

#### Phase 2: User Model & CRUD (Day 2)
- [ ] Create User model with Sequelize
- [ ] Implement password hashing
- [ ] Create user routes
- [ ] Implement CRUD operations

#### Phase 3: Authentication (Day 3)
- [ ] Implement JWT generation
- [ ] Create auth middleware
- [ ] Add login endpoint
- [ ] Protect routes

#### Phase 4: Validation & Error Handling (Day 4)
- [ ] Add input validation
- [ ] Implement error handling middleware
- [ ] Add request logging
- [ ] Write tests

---

## Step 3: EXECUTE

### Phase 1: Express Setup

```javascript
// src/app.js
const express = require('express');
const helmet = require('helmet');
const cors = require('cors');
const morgan = require('morgan');
const { errorHandler } = require('./middleware/errorHandler');
const userRoutes = require('./routes/users');

const app = express();

// Security middleware
app.use(helmet());
app.use(cors());

// Body parsing
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Logging
app.use(morgan('combined'));

// Routes
app.use('/api/users', userRoutes);

// Health check
app.get('/health', (req, res) => {
    res.json({ status: 'OK', timestamp: new Date().toISOString() });
});

// Error handling
app.use(errorHandler);

module.exports = app;
```

### Phase 2: User Model

```javascript
// src/models/User.js
const { DataTypes } = require('sequelize');
const bcrypt = require('bcrypt');
const sequelize = require('../config/database');

const User = sequelize.define('User', {
    id: {
        type: DataTypes.UUID,
        defaultValue: DataTypes.UUIDV4,
        primaryKey: true
    },
    email: {
        type: DataTypes.STRING,
        allowNull: false,
        unique: true,
        validate: {
            isEmail: true
        }
    },
    password: {
        type: DataTypes.STRING,
        allowNull: false
    },
    name: {
        type: DataTypes.STRING,
        allowNull: false
    },
    role: {
        type: DataTypes.ENUM('user', 'admin'),
        defaultValue: 'user'
    }
}, {
    hooks: {
        beforeCreate: async (user) => {
            user.password = await bcrypt.hash(user.password, 12);
        },
        beforeUpdate: async (user) => {
            if (user.changed('password')) {
                user.password = await bcrypt.hash(user.password, 12);
            }
        }
    }
});

User.prototype.validatePassword = async function(password) {
    return bcrypt.compare(password, this.password);
};

User.prototype.toJSON = function() {
    const values = { ...this.get() };
    delete values.password;
    return values;
};

module.exports = User;
```

### Phase 3: Authentication

```javascript
// src/utils/jwt.js
const jwt = require('jsonwebtoken');

const JWT_SECRET = process.env.JWT_SECRET;
const JWT_EXPIRES_IN = '1h';
const REFRESH_EXPIRES_IN = '7d';

const generateTokens = (user) => {
    const accessToken = jwt.sign(
        { userId: user.id, role: user.role },
        JWT_SECRET,
        { expiresIn: JWT_EXPIRES_IN }
    );
    
    const refreshToken = jwt.sign(
        { userId: user.id, type: 'refresh' },
        JWT_SECRET,
        { expiresIn: REFRESH_EXPIRES_IN }
    );
    
    return { accessToken, refreshToken };
};

const verifyToken = (token) => {
    return jwt.verify(token, JWT_SECRET);
};

module.exports = { generateTokens, verifyToken };

// src/middleware/auth.js
const { verifyToken } = require('../utils/jwt');
const { AppError } = require('./errorHandler');

const authenticate = async (req, res, next) => {
    try {
        const authHeader = req.headers.authorization;
        
        if (!authHeader || !authHeader.startsWith('Bearer ')) {
            throw new AppError('Authentication required', 401);
        }
        
        const token = authHeader.split(' ')[1];
        const decoded = verifyToken(token);
        
        req.user = decoded;
        next();
    } catch (error) {
        next(new AppError('Invalid token', 401));
    }
};

const authorize = (...roles) => {
    return (req, res, next) => {
        if (!roles.includes(req.user.role)) {
            return next(new AppError('Insufficient permissions', 403));
        }
        next();
    };
};

module.exports = { authenticate, authorize };
```

### Phase 4: Controller & Routes

```javascript
// src/controllers/userController.js
const User = require('../models/User');
const { generateTokens } = require('../utils/jwt');
const { AppError } = require('../middleware/errorHandler');

const register = async (req, res, next) => {
    try {
        const { email, password, name } = req.body;
        
        const existingUser = await User.findOne({ where: { email } });
        if (existingUser) {
            throw new AppError('Email already registered', 409);
        }
        
        const user = await User.create({ email, password, name });
        const tokens = generateTokens(user);
        
        res.status(201).json({
            success: true,
            data: { user, ...tokens }
        });
    } catch (error) {
        next(error);
    }
};

const login = async (req, res, next) => {
    try {
        const { email, password } = req.body;
        
        const user = await User.findOne({ where: { email } });
        if (!user || !(await user.validatePassword(password))) {
            throw new AppError('Invalid credentials', 401);
        }
        
        const tokens = generateTokens(user);
        
        res.json({
            success: true,
            data: { user, ...tokens }
        });
    } catch (error) {
        next(error);
    }
};

const getUsers = async (req, res, next) => {
    try {
        const users = await User.findAll();
        res.json({
            success: true,
            data: users
        });
    } catch (error) {
        next(error);
    }
};

const getUser = async (req, res, next) => {
    try {
        const user = await User.findByPk(req.params.id);
        if (!user) {
            throw new AppError('User not found', 404);
        }
        res.json({
            success: true,
            data: user
        });
    } catch (error) {
        next(error);
    }
};

const updateUser = async (req, res, next) => {
    try {
        const user = await User.findByPk(req.params.id);
        if (!user) {
            throw new AppError('User not found', 404);
        }
        
        // Only allow updating own profile (or admin)
        if (req.user.userId !== user.id && req.user.role !== 'admin') {
            throw new AppError('Not authorized', 403);
        }
        
        await user.update(req.body);
        res.json({
            success: true,
            data: user
        });
    } catch (error) {
        next(error);
    }
};

const deleteUser = async (req, res, next) => {
    try {
        const user = await User.findByPk(req.params.id);
        if (!user) {
            throw new AppError('User not found', 404);
        }
        
        await user.destroy();
        res.status(204).send();
    } catch (error) {
        next(error);
    }
};

module.exports = { register, login, getUsers, getUser, updateUser, deleteUser };

// src/routes/users.js
const express = require('express');
const router = express.Router();
const { body, param } = require('express-validator');
const { validate } = require('../middleware/validate');
const { authenticate, authorize } = require('../middleware/auth');
const userController = require('../controllers/userController');

// Validation rules
const registerValidation = [
    body('email').isEmail().normalizeEmail(),
    body('password').isLength({ min: 8 }),
    body('name').trim().isLength({ min: 2, max: 100 })
];

const loginValidation = [
    body('email').isEmail().normalizeEmail(),
    body('password').notEmpty()
];

// Public routes
router.post('/register', registerValidation, validate, userController.register);
router.post('/login', loginValidation, validate, userController.login);

// Protected routes
router.use(authenticate);

router.get('/', userController.getUsers);
router.get('/:id', param('id').isUUID(), validate, userController.getUser);
router.put('/:id', param('id').isUUID(), validate, userController.updateUser);
router.delete('/:id', authorize('admin'), param('id').isUUID(), validate, userController.deleteUser);

module.exports = router;
```

---

## Step 4: ITERATE

### Evaluation

After implementing, run tests:

```bash
npm test -- --coverage
```

### Results
```
✓ POST /api/users/register - creates user (85ms)
✓ POST /api/users/login - returns tokens (45ms)
✓ GET /api/users - returns all users (32ms)
✓ GET /api/users/:id - returns user (28ms)
✓ PUT /api/users/:id - updates user (52ms)
✓ DELETE /api/users/:id - deletes user (admin only) (38ms)

Coverage: 92%
```

### Issues Found & Fixed
1. ⚠️ Missing rate limiting on login endpoint → Added express-rate-limit
2. ⚠️ No refresh token rotation → Implemented token rotation on refresh
3. ⚠️ Missing CORS configuration for production → Added proper CORS config

### Final Commit
```
feat(api): implement user management REST API

Complete implementation of user management API with:
- CRUD operations for users
- JWT authentication with refresh tokens
- Input validation using express-validator
- Comprehensive error handling
- Rate limiting on auth endpoints
- 92% test coverage

Closes #1
```

---

## Key Learnings

1. **Follow the APEI cycle** - Analysis before coding prevented security issues
2. **Input validation is critical** - express-validator saved time on edge cases
3. **Test as you go** - Caught the refresh token issue early
4. **Security first** - helmet, bcrypt, and rate limiting from the start

## Related Prompts Used

- [API Development Prompt](../project-types/api-development-prompt.md)
- [Security Audit Prompt](../agents/security-audit-prompt.md)
- [Testing Strategies Prompt](../agents/testing-strategies-prompt.md)
