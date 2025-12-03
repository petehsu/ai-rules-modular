# Testing Standards & Patterns

## 1. Test Coverage Requirements

### Coverage by Module Type
- **Critical Business Logic:** 80%+ coverage (payments, auth, data validation)
- **Utility Functions:** 100% coverage
- **UI Components:** Core interaction paths tested
- **API Endpoints:** 80%+ coverage
- **Complex Algorithms:** 100% coverage

### Priority Levels
1. **MUST TEST:**
   - Payment/order flows
   - Authorization checks
   - Data validation logic
   - Error handling paths

2. **SHOULD TEST:**
   - API endpoints
   - Complex algorithms
   - State management

3. **MAY TEST:**
   - Static pages
   - Simple CRUD operations

---

## 2. Unit Testing

### General Standards
- **Naming Convention:** `test('should <expected behavior> when <condition>', ...)`
- **AAA Pattern:** Arrange → Act → Assert
- **Co-location:** Test files next to source: `Button.tsx` → `Button.test.tsx`

### JavaScript/TypeScript (Jest + Testing Library)
```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from './Button';

test('should call onClick when clicked', () => {
  // Arrange
  const handleClick = jest.fn();
  render(<Button onClick={handleClick}>Click me</Button>);
  
  // Act
  fireEvent.click(screen.getByText('Click me'));
  
  // Assert
  expect(handleClick).toHaveBeenCalledTimes(1);
});
```

### Python (pytest)
```python
import pytest
from myapp.calculator import calculate_discount

def test_should_calculate_20_percent_discount():
    # Arrange
    price = 100
    discount_percent = 20
    
    # Act
    result = calculate_discount(price, discount_percent)
    
    # Assert
    assert result == 80

def test_should_raise_error_for_negative_price():
    # Arrange & Act & Assert
    with pytest.raises(ValueError, match="Invalid input"):
        calculate_discount(-100, 20)
```

### Java (JUnit 5)
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class UserServiceTest {
    @Test
    void shouldReturnUserWhenIdExists() {
        // Arrange
        UserService service = new UserService();
        
        // Act
        User user = service.getUser("123");
        
        // Assert
        assertNotNull(user);
        assertEquals("123", user.getId());
    }
}
```

### Kotlin (JUnit + MockK)
```kotlin
import io.mockk.*
import org.junit.Test
import kotlin.test.assertEquals

class UserViewModelTest {
    @Test
    fun `loadUser should update state to success when api succeeds`() = runTest {
        // Arrange
        val mockRepository = mockk<UserRepository>()
        coEvery { mockRepository.getUser(any()) } returns testUser
        val viewModel = UserViewModel(mockRepository)
        
        // Act
        viewModel.loadUser("123")
        advanceUntilIdle()
        
        // Assert
        val state = viewModel.uiState.value
        assertTrue(state is UiState.Success)
        assertEquals(testUser, (state as UiState.Success).data)
    }
}
```

---

## 3. Integration Testing

### API Testing (Node.js + Supertest)
```typescript
import request from 'supertest';
import app from './app';

describe('POST /api/users', () => {
  it('should create a new user', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({
        email: 'test@example.com',
        password: 'securePassword123'
      });
    
    expect(response.status).toBe(201);
    expect(response.body).toHaveProperty('id');
    expect(response.body.email).toBe('test@example.com');
  });
});
```

### API Testing (Python + TestClient)
```python
from fastapi.testclient import TestClient
from myapp.main import app

client = TestClient(app)

def test_create_user():
    response = client.post(
        "/api/users",
        json={"email": "test@example.com", "password": "securePassword123"}
    )
    assert response.status_code == 201
    assert "id" in response.json()
    assert response.json()["email"] == "test@example.com"
```

### Database Testing
**Use Test Containers or In-Memory Databases:**
- **Node.js:** SQLite in-memory for development, Testcontainers for CI
- **Python:** SQLite in-memory or pytest-postgresql
- **Java:** H2 in-memory or Testcontainers

---

## 4. End-to-End (E2E) Testing

### Playwright (Modern Choice)
```typescript
import { test, expect } from '@playwright/test';

test('user can login successfully', async ({ page }) => {
  await page.goto('https://example.com/login');
  
  await page.fill('input[name="email"]', 'user@example.com');
  await page.fill('input[name="password"]', 'password123');
  await page.click('button[type="submit"]');
  
  await expect(page).toHaveURL('https://example.com/dashboard');
  await expect(page.locator('h1')).toContainText('Welcome');
});
```

### Cypress (Alternative)
```javascript
describe('Login Flow', () => {
  it('should login successfully', () => {
    cy.visit('/login');
    cy.get('input[name="email"]').type('user@example.com');
    cy.get('input[name="password"]').type('password123');
    cy.get('button[type="submit"]').click();
    
    cy.url().should('include', '/dashboard');
    cy.contains('h1', 'Welcome');
  });
});
```

---

## 5. Test-Driven Development (TDD) Pattern

**When implementing critical features:**

### Step 1: Write Failing Test
```typescript
test('should calculate total with tax', () => {
  const total = calculateTotalWithTax([
    { price: 100, quantity: 2 }
  ], 0.1);
  expect(total).toBe(220); // 200 + 20 tax
});
```

### Step 2: Implement Minimal Code
```typescript
function calculateTotalWithTax(items: Item[], taxRate: number): number {
  const subtotal = items.reduce((sum, item) => sum + item.price * item.quantity, 0);
  return subtotal + (subtotal * taxRate);
}
```

### Step 3: Refactor
Add error handling, type safety, edge case handling.

---

## 6. Mocking & Stubbing

### Mock External APIs
```typescript
import { jest } from '@jest/globals';

// Mock fetch
global.fetch = jest.fn(() =>
  Promise.resolve({
    ok: true,
    json: async () => ({ id: '123', name: 'John' }),
  })
) as jest.Mock;

test('should fetch user data', async () => {
  const user = await fetchUser('123');
  expect(user.name).toBe('John');
  expect(fetch).toHaveBeenCalledWith('/api/users/123');
});
```

### Mock Database Queries (Python)
```python
from unittest.mock import patch, MagicMock

@patch('myapp.database.query')
def test_get_user(mock_query):
    # Arrange
    mock_query.return_value = {"id": "123", "name": "John"}
    
    # Act
    user = get_user("123")
    
    # Assert
    assert user["name"] == "John"
    mock_query.assert_called_once_with("SELECT * FROM users WHERE id = ?", "123")
```

---

## 7. Test Organization

### Directory Structure
```
src/
├── components/
│   ├── Button.tsx
│   └── Button.test.tsx
├── services/
│   ├── userService.ts
│   └── userService.test.ts
└── utils/
    ├── validation.ts
    └── validation.test.ts

tests/
├── integration/
│   └── api/
│       └── users.test.ts
└── e2e/
    └── login.spec.ts
```

---

## 8. Testing Checklist

Before merging code, verify:
- [ ] All critical paths have tests
- [ ] Tests follow AAA pattern
- [ ] Mocks are properly configured
- [ ] No hardcoded values in tests
- [ ] Tests are isolated (no inter-test dependencies)
- [ ] Edge cases covered (null, empty, invalid input)
- [ ] Error handling paths tested
