# General Backend Rules

## 1. Database Standards

### 1.1 SQL (PostgreSQL/MySQL)
**Standards:**
- ✅ Use ORM (Prisma/TypeORM/SQLAlchemy)
- ✅ Must index these fields:
  - Foreign keys
  - Fields frequently used in WHERE clauses
  - ORDER BY fields
- ✅ Use transactions:
  ```typescript
  await prisma.$transaction(async (tx) => {
    await tx.order.create({ data: orderData });
    await tx.inventory.update({ 
      where: { id }, 
      data: { stock: { decrement: 1 } }
    });
  });
  ```

### 1.2 NoSQL (MongoDB/Redis)
**Standards:**
- ✅ MongoDB: Design schema for query patterns
- ✅ Redis: Set expiration time:
  ```javascript
  await redis.setex(`session:${userId}`, 3600, sessionData);
  ```

---

## 2. DevOps & Deployment

### 2.1 Docker
**Dockerfile Standards:**
- Use Multi-stage builds to reduce image size.
- Run as non-root user.

### 2.2 CI/CD
**Standards:**
- ✅ Pipeline: Lint → Test → Build → Deploy
- ✅ Production deployment requires manual approval
- ✅ Environment variables managed via Secrets

---

## 3. Backend Performance Patterns

1. **Database Queries:**
   - Use `select` to specify fields (avoid `SELECT *`).
   - Solve N+1 query problem with JOIN or DataLoader.
   - Paginated queries for large datasets.

2. **Caching Strategy:**
   - Check cache -> Fetch DB -> Set cache (with TTL).

3. **Concurrent Processing:**
   - Use `Promise.all` for independent async operations.

---

## 4. API Documentation

**Backend APIs must generate OpenAPI/Swagger documentation:**

```typescript
/**
 * Get user information
 * @route GET /api/users/:id
 * @param {string} id - User ID
 * @returns {User} User object
 * @throws {404} User not found
 * @throws {500} Server error
 */
```

---

## 5. Monitoring & Observability

### 5.1 Logging
- **Info:** User actions, system events (with structured data).
- **Error:** Stack traces, context (orderId, userId).

### 5.2 Error Tracking
- Use Sentry or similar.
- Capture exceptions with context tags.
- Remove sensitive data (PII, secrets) before sending.
