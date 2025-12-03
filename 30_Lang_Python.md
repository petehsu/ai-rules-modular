# Python Language Rules

## 1. Project Structure (FastAPI/Django/Flask)
```
project/
├── api/
├── services/
├── models/
├── schemas/
└── tests/
```

## 2. Standards
- ✅ **Type Hints:** 100% coverage required.
- ✅ **Validation:** Use Pydantic for data validation.
  ```python
  from pydantic import BaseModel, EmailStr, conint, Field
  
  class UserCreate(BaseModel):
      email: EmailStr
      age: conint(ge=18, le=120)
      password: str = Field(min_length=8)
  ```
- ✅ **Async-first (FastAPI):**
  ```python
  @app.get("/users/{user_id}")
  async def get_user(user_id: int, db: AsyncSession = Depends(get_db)):
      result = await db.execute(select(User).where(User.id == user_id))
      return result.scalar_one_or_none()
  ```

## 3. Error Handling
- ❌ **Bad:** Bare `except:`
- ✅ **Good:** Catch specific exceptions and log them.
  ```python
  def read_config() -> Optional[dict]:
      try:
          with open('config.json') as f:
              return json.load(f)
      except (json.JSONDecodeError, IOError) as e:
          logger.error(f"Failed to read config: {e}")
          return None
  ```
