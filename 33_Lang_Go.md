# Go Language Rules

## 1. Project Structure
```
project/
├── cmd/
├── internal/
│   ├── handler/
│   ├── service/
│   └── repository/
├── pkg/
└── api/
```

## 2. Standards
- ✅ **Formatting:** Use `gofmt`.
- ✅ **Error Handling:** Explicit error checking, no panic.
  ```go
  func GetUser(id int) (*User, error) {
      user, err := db.Query("SELECT * FROM users WHERE id = ?", id)
      if err != nil {
          return nil, fmt.Errorf("failed to get user: %w", err)
      }
      return user, nil
  }
  ```
