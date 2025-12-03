# Edge Cases & Special Scenarios

## 1. Handling Legacy Code

### 1.1 Identify Tech Stack Version
When user provides old code for upgrade:

1. **Detect Version:**
   - React 16 → React 18
   - Vue 2 → Vue 3
   - Python 2.7 → Python 3.10+
   - Java 8 → Java 17+

2. **Progressive Migration:**
   ```
   I notice this is React 16 code. I suggest a step-by-step upgrade:
   
   Step 1: Update dependency versions
   Step 2: Replace deprecated APIs (componentWillMount → useEffect)
   Step 3: Add TypeScript types
   Step 4: Optimize performance (React.memo, useMemo)
   
   Which step should I start with?
   ```

### 1.2 Refactoring Strategy
- **Don't rewrite everything at once**
- Use [Strangler Fig Pattern](https://martinfowler.com/bliki/StranglerFigApplication.html): Gradually replace old code
- Maintain backward compatibility during transition

---

## 2. Multi-Person Collaboration Projects

### 2.1 Stricter Type Definitions
When code will be modified by multiple people:

```typescript
// ❌ Loose - Hard to maintain
type Config = Record<string, any>;

// ✅ Strict - Clear contract
type Config = {
  apiUrl: string;
  timeout: number;
  retries?: number;
};
```

### 2.2 Detailed JSDoc
```typescript
/**
 * Calculate order total
 * 
 * @param items - Array of order items
 * @param taxRate - Tax rate, range 0-1
 * @returns Total price with tax, rounded to 2 decimals
 * 
 * @example
 * ```ts
 * const total = calculateTotal(
 *   [{ price: 100, quantity: 2 }],
 *   0.1
 * );
 * // Returns 220 (200 + 20 tax)
 * ```
 */
```

---

## 3. Performance-Sensitive Scenarios

When user explicitly mentions "high performance" or "large data volume":

### 3.1 Data Structure Selection
```javascript
// ❌ Array lookup O(n)
const user = users.find(u => u.id === targetId);

// ✅ Map lookup O(1)
const userMap = new Map(users.map(u => [u.id, u]));
const user = userMap.get(targetId);
```

### 3.2 Avoid Unnecessary Computation
```javascript
// ❌ Recalculate every render
function Component({ items }) {
  const total = items.reduce((sum, item) => sum + item.price, 0);
  return <div>{total}</div>;
}

// ✅ Cache calculation result
function Component({ items }) {
  const total = useMemo(
    () => items.reduce((sum, item) => sum + item.price, 0),
    [items]
  );
  return <div>{total}</div>;
}
```

### 3.3 Database Query Optimization
```sql
-- ❌ Subquery inefficient
SELECT * FROM users 
WHERE id IN (SELECT user_id FROM orders WHERE status = 'paid');

-- ✅ JOIN more efficient
SELECT DISTINCT u.* FROM users u
INNER JOIN orders o ON u.id = o.user_id
WHERE o.status = 'paid';
```

---

## 4. Internationalization (i18n) Projects

### 4.1 Externalize Strings
```typescript
// ❌ Hardcoded text
<button>Submit</button>

// ✅ Use i18n
import { useTranslation } from 'react-i18next';
const { t } = useTranslation();
<button>{t('common.submit')}</button>
```

### 4.2 Date/Number Formatting
```typescript
const formatter = new Intl.NumberFormat('zh-CN', {
  style: 'currency',
  currency: 'CNY'
});
formatter.format(1234.56); // ¥1,234.56
```

### 4.3 Pluralization
```javascript
// en.json
{
  "items": "{{count}} item",
  "items_plural": "{{count}} items"
}

// Usage
t('items', { count: 1 }); // "1 item"
t('items', { count: 5 }); // "5 items"
```

---

## 5. Real-time Applications (WebSocket/SSE)

For chat, notifications, collaborative editing:

### 5.1 WebSocket with Reconnection
```typescript
class RealtimeService {
  private ws: WebSocket | null = null;
  
  connect(url: string) {
    this.ws = new WebSocket(url);
    
    this.ws.onopen = () => {
      console.log('Connected');
      this.heartbeat();
    };
    
    this.ws.onmessage = (event) => {
      const data = JSON.parse(event.data);
      this.handleMessage(data);
    };
    
    this.ws.onerror = (error) => {
      console.error('WebSocket error:', error);
    };
    
    this.ws.onclose = () => {
      console.log('Disconnected, reconnecting...');
      setTimeout(() => this.connect(url), 3000);
    };
  }
  
  private heartbeat() {
    setInterval(() => {
      if (this.ws?.readyState === WebSocket.OPEN) {
        this.ws.send(JSON.stringify({ type: 'ping' }));
      }
    }, 30000);
  }
}
```

### 5.2 Server-Sent Events (SSE)
```typescript
const eventSource = new EventSource('/api/events');

eventSource.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log('Received:', data);
};

eventSource.onerror = (error) => {
  console.error('SSE error:', error);
  eventSource.close();
};
```

---

## 6. Handling Uncertainty

### 6.1 When Requirements are Unclear
```
Before starting, I need to confirm a few details:

1. User authentication method: JWT / Session / OAuth?
2. Database: PostgreSQL / MySQL / MongoDB?
3. Deployment environment: Vercel / AWS / Self-hosted?

These will affect the technology choices. Please tell me your preferences.
```

### 6.2 When Tech Stack is Outdated
```
⚠️ Notice: The React 16 you're using is no longer maintained.

Recommend upgrading to React 18, main improvements:
- Concurrent rendering
- Automatic batching
- Suspense support

Would you like me to create a migration plan?
```

---

## 7. Monorepo Projects

### 7.1 Workspace Structure (pnpm/yarn workspaces)
```
monorepo/
├── apps/
│   ├── web/         (Next.js)
│   └── mobile/      (React Native)
├── packages/
│   ├── ui/          (Shared components)
│   ├── utils/       (Shared utilities)
│   └── types/       (Shared TypeScript types)
└── pnpm-workspace.yaml
```

### 7.2 Shared Dependencies
- Use `workspace:*` protocol for internal packages
- Single version for external dependencies (avoid conflicts)

---

## 8. GraphQL vs REST

### 8.1 When to Use GraphQL
- **Over-fetching/Under-fetching:** Client needs flexible data shapes
- **Multiple Resources:** Single query fetches related data
- **Rapid Iteration:** Schema evolves frequently

### 8.2 When to Use REST
- **Simple CRUD:** Standard create/read/update/delete operations
- **Caching:** HTTP caching works out of the box
- **File Uploads:** Easier with multipart/form-data

---

## 9. Microservices Communication

### 9.1 Synchronous (REST/gRPC)
- **REST:** Human-readable, easy debugging
- **gRPC:** High performance, binary protocol, strong typing

### 9.2 Asynchronous (Message Queue)
- **Use Cases:** Event-driven, decoupling services
- **Tools:** RabbitMQ, Kafka, Redis Pub/Sub

---

## 10. Mobile-Specific Edge Cases

### 10.1 Offline-First Apps
```typescript
// Check network status
if (!navigator.onLine) {
  // Fallback to cached data
  const cachedData = await localDB.get(key);
  return cachedData;
}
```

### 10.2 Platform-Specific Code (React Native)
```typescript
import { Platform } from 'react-native';

const styles = StyleSheet.create({
  container: {
    paddingTop: Platform.OS === 'ios' ? 20 : 0,
  },
});
```

---

## 11. Security Edge Cases

### 11.1 Rate Limiting
```typescript
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // Max 100 requests per window
});

app.use('/api/', limiter);
```

### 11.2 CSRF Protection
```typescript
import csrf from 'csurf';

const csrfProtection = csrf({ cookie: true });
app.post('/api/payment', csrfProtection, (req, res) => {
  // Protected route
});
```
