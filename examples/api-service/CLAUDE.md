# API Service Module - Architecture & Patterns

## 📍 Breadcrumbs

- **New to the project?** → [Root CLAUDE.md](../../CLAUDE.md) for setup and overview
- **Looking for strategic context?** → [ROADMAP.md](../../ROADMAP.md)
- **Looking for current sprint work?** → [PROJECT_PLAN.md](../../PROJECT_PLAN.md)
- **Looking for other modules?** → [Root CLAUDE.md - Documentation Navigation](../../CLAUDE.md#-documentation-navigation)

---

## When to Read This Doc

**Read this document when**:
- Building or modifying API endpoints in this service
- Understanding the request/response flow
- Integrating with external services through this API
- Debugging API-related issues
- Adding new authentication/authorization logic

**Skip this document if**:
- You just need to set up the project → See [root CLAUDE.md](../../CLAUDE.md)
- You're working on [other module] → See `[path/to/other/CLAUDE.md]`
- You need database schema info → See `[path/to/models/CLAUDE.md]`

---

## Module Overview

**Purpose**: The API service provides RESTful endpoints for [describe what the API does - e.g., user management, data processing, etc.].

**Key Responsibilities**:
- Request validation and sanitization
- Business logic orchestration
- Response formatting
- Error handling and logging
- Rate limiting and throttling

**Not Responsible For**:
- Database schema definitions (see `[models folder]`)
- Frontend rendering (see `[frontend folder]`)
- Background job processing (see `[jobs folder]`)

---

## Architecture

### Request Flow

```
Client Request
    ↓
┌─────────────────────────────────────────────────────────────┐
│ 1. Middleware Layer                                         │
│    • Authentication (verify tokens)                         │
│    • Rate Limiting (check request quotas)                   │
│    • Request Logging                                        │
└─────────────────────────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────────────────────────┐
│ 2. Route Handler                                            │
│    • Route matching                                         │
│    • Parameter extraction                                   │
└─────────────────────────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────────────────────────┐
│ 3. Validation Layer                                         │
│    • Schema validation (request body, params, query)        │
│    • Business rule validation                               │
└─────────────────────────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────────────────────────┐
│ 4. Service Layer                                            │
│    • Business logic execution                               │
│    • Database operations (via repository pattern)           │
│    • External API calls                                     │
└─────────────────────────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────────────────────────┐
│ 5. Response Layer                                           │
│    • Response formatting                                    │
│    • Error serialization                                    │
│    • Status code selection                                  │
└─────────────────────────────────────────────────────────────┘
    ↓
Client Response
```

### Component Structure

```
api-service/
├── routes/               # Route definitions and handlers
│   ├── __init__.py       # Route registration
│   ├── users.py          # User-related endpoints
│   ├── items.py          # Item-related endpoints
│   └── health.py         # Health check endpoints
│
├── middleware/           # Request/response middleware
│   ├── auth.py           # Authentication middleware
│   ├── rate_limit.py     # Rate limiting
│   └── logging.py        # Request/response logging
│
├── validators/           # Request validation schemas
│   ├── user_schemas.py   # User request/response schemas
│   └── item_schemas.py   # Item request/response schemas
│
├── services/             # Business logic layer
│   ├── user_service.py   # User business logic
│   └── item_service.py   # Item business logic
│
├── serializers/          # Response formatting
│   ├── user_serializer.py
│   └── item_serializer.py
│
└── utils/                # API utilities
    ├── errors.py         # Custom error classes
    └── responses.py      # Response helpers
```

---

## Design Patterns

### 1. Repository Pattern for Data Access

**Why**: Decouples business logic from database implementation, makes testing easier.

**Example**:
```python
# Bad: Business logic directly accessing database
def get_user(user_id):
    user = db.session.query(User).filter_by(id=user_id).first()
    if not user:
        raise NotFoundError()
    return user

# Good: Using repository pattern
def get_user(user_id):
    user = user_repository.find_by_id(user_id)
    if not user:
        raise NotFoundError()
    return user
```

**Location**: Services use repositories from `[repository folder]`

### 2. Dependency Injection for Services

**Why**: Makes components testable and loosely coupled.

**Example**:
```python
# Bad: Hard-coded dependencies
class UserService:
    def __init__(self):
        self.repo = UserRepository()
        self.email_service = EmailService()

# Good: Injected dependencies
class UserService:
    def __init__(self, user_repo, email_service):
        self.repo = user_repo
        self.email_service = email_service
```

**Location**: See `services/` folder for implementation

### 3. Schema-Based Validation

**Why**: Centralized validation logic, automatic error messages, type safety.

**Example**:
```python
from pydantic import BaseModel, validator

class CreateUserRequest(BaseModel):
    email: str
    username: str
    age: int

    @validator('email')
    def email_must_be_valid(cls, v):
        if '@' not in v:
            raise ValueError('Invalid email format')
        return v
```

**Location**: `validators/` folder for all schemas

### 4. Consistent Error Handling

**Why**: Predictable error responses, easier debugging, better client experience.

**Error Response Format**:
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request parameters",
    "details": [
      {
        "field": "email",
        "message": "Email format is invalid"
      }
    ]
  }
}
```

**Implementation**: `utils/errors.py` defines custom exception classes, middleware catches and formats them.

---

## Common Tasks

### Adding a New API Endpoint

1. **Define route** in appropriate file in `routes/`
   ```python
   @router.post("/items", status_code=201)
   async def create_item(item: CreateItemRequest):
       # Implementation
   ```

2. **Create validation schema** in `validators/`
   ```python
   class CreateItemRequest(BaseModel):
       name: str
       price: float
   ```

3. **Implement business logic** in `services/`
   ```python
   class ItemService:
       def create_item(self, data):
           # Business logic here
   ```

4. **Add tests**:
   - Unit tests: `tests/unit/services/test_item_service.py`
   - Integration tests: `tests/integration/api/test_items.py`

5. **Update documentation**:
   - If it changes architecture, update this file
   - Add to `CHANGELOG.md` when releasing

### Implementing Authentication

**Pattern**: Token-based authentication using JWT

1. **Middleware location**: `middleware/auth.py`
2. **Token validation**: Checks signature and expiration
3. **User injection**: Adds `current_user` to request context

**Usage in routes**:
```python
from middleware.auth import require_auth

@router.get("/protected")
@require_auth
async def protected_route(request):
    user = request.state.current_user
    # Use authenticated user
```

### Handling Rate Limiting

**Pattern**: Token bucket algorithm with Redis backend

**Configuration**: `middleware/rate_limit.py:10-15`

**Default limits**:
- Anonymous: 100 requests/hour
- Authenticated: 1000 requests/hour
- Admin: Unlimited

**Custom limits**:
```python
@router.post("/expensive-operation")
@rate_limit(max_requests=10, window=3600)
async def expensive_route():
    # Limited to 10 requests/hour
```

### Adding External API Integration

1. **Create service client** in `services/external/[service_name].py`
2. **Implement retry logic** using exponential backoff
3. **Add timeout handling** (default: 10 seconds)
4. **Cache responses** if appropriate
5. **Add circuit breaker** for critical services

**Example**:
```python
class ExternalAPIClient:
    def __init__(self, api_key, base_url, timeout=10):
        self.api_key = api_key
        self.base_url = base_url
        self.timeout = timeout

    @retry(max_attempts=3, backoff=2)
    async def fetch_data(self, endpoint):
        # Implementation with error handling
```

---

## Integration Guide

### Integrating with Database Layer

**Pattern**: Services use repository pattern

```python
# In your service
from repositories.user_repository import UserRepository

class UserService:
    def __init__(self, user_repo: UserRepository):
        self.user_repo = user_repo

    def get_user(self, user_id):
        return self.user_repo.find_by_id(user_id)
```

**See**: `[path/to/repositories/CLAUDE.md]` for repository implementation details

### Integrating with Background Jobs

**Pattern**: Services publish events, job workers consume them

```python
# In your service
from events.publisher import EventPublisher

class OrderService:
    def create_order(self, order_data):
        order = self.repo.create(order_data)
        # Publish event for async processing
        EventPublisher.publish('order.created', {'order_id': order.id})
        return order
```

**See**: `[path/to/jobs/CLAUDE.md]` for job worker implementation

### Integrating with Frontend

**API Documentation**: Auto-generated OpenAPI docs at `/api/docs`

**CORS Configuration**: `middleware/cors.py`

**Response Format**: All responses follow JSON:API specification

---

## Testing Strategy

### Unit Tests

**Focus**: Individual components in isolation

**Location**: `tests/unit/api-service/`

**Example**:
```python
def test_user_service_create():
    # Mock repository
    mock_repo = Mock(spec=UserRepository)
    mock_repo.create.return_value = User(id=1, email="test@example.com")

    # Test service
    service = UserService(mock_repo)
    user = service.create_user({"email": "test@example.com"})

    assert user.id == 1
    mock_repo.create.assert_called_once()
```

### Integration Tests

**Focus**: Full request/response cycle

**Location**: `tests/integration/api/`

**Example**:
```python
def test_create_user_endpoint(client):
    response = client.post("/users", json={
        "email": "test@example.com",
        "username": "testuser"
    })

    assert response.status_code == 201
    assert response.json()["email"] == "test@example.com"
```

---

## Performance Considerations

### 1. Database Query Optimization

- **Use select_related/prefetch_related** for avoiding N+1 queries
- **Add indexes** on frequently queried fields
- **Implement pagination** for list endpoints (default: 50 items/page)

### 2. Caching Strategy

**What to cache**:
- User permissions (TTL: 5 minutes)
- Configuration data (TTL: 1 hour)
- External API responses (TTL: varies)

**Implementation**: Redis-backed cache, see `utils/cache.py`

### 3. Response Time Targets

- Simple queries: < 100ms
- Complex queries: < 500ms
- External API calls: < 2s (with timeout)

---

## Known Issues & Gotchas

### ✅ RESOLVED: Async Database Connections

**Issue**: Deadlocks when using synchronous database calls in async routes

**Solution**: Use `asyncpg` for all database operations in async routes

**Location**: `repositories/base.py:45`

### ⚠️ KNOWN LIMITATION: Rate Limiting Accuracy

**Issue**: Distributed rate limiting with Redis may have slight inaccuracies under very high load

**Impact**: Actual limits might be 1-2% higher than configured

**Mitigation**: Set limits slightly lower than hard requirements

---

## Debugging Tips

### Enabling Debug Logging

```bash
# Set environment variable
export LOG_LEVEL=DEBUG

# Or in .env file
LOG_LEVEL=DEBUG
```

### Common Error Patterns

**Error**: `ValidationError: field required`
- **Cause**: Missing required field in request
- **Fix**: Check `validators/` for schema definition

**Error**: `AuthenticationError: Invalid token`
- **Cause**: Expired or malformed JWT
- **Fix**: Check token generation and expiration settings

**Error**: `RateLimitExceeded`
- **Cause**: Too many requests in time window
- **Fix**: Implement exponential backoff in client

---

## Additional Resources

### Internal Documentation
- **[Root CLAUDE.md](../../CLAUDE.md)**: Project setup and overview
- **[ROADMAP.md](../../ROADMAP.md)**: Strategic vision for API evolution
- **[PROJECT_PLAN.md](../../PROJECT_PLAN.md)**: Current API development sprint

### Related Modules
- **Database/Models**: `[path/to/models/CLAUDE.md]`
- **Authentication**: `[path/to/auth/CLAUDE.md]`
- **Background Jobs**: `[path/to/jobs/CLAUDE.md]`

### External Resources
- **Framework Documentation**: [Link to your framework docs]
- **API Best Practices**: [Link to internal or external API guidelines]

---

**Last Updated**: [YYYY-MM-DD]
**Status**: [e.g., "Production ready", "Under active development"]
**Maintainer**: [Name or team]

---

**Related Documentation**:
- [Root CLAUDE.md](../../CLAUDE.md) - Project overview and setup
- [ROADMAP.md](../../ROADMAP.md) - Strategic vision
- [PROJECT_PLAN.md](../../PROJECT_PLAN.md) - Current sprint work
