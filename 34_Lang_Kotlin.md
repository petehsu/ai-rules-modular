# Kotlin Language Rules

## 1. Project Structure

### 1.1 Android
```
app/src/main/kotlin/com/company/app/
├── ui/
│   ├── screens/
│   └── components/
├── data/
│   ├── repository/
│   ├── api/
│   └── local/
├── domain/
│   ├── model/
│   └── usecase/
└── di/
```

### 1.2 Backend (Ktor)
```
src/main/kotlin/
├── Application.kt
├── plugins/
├── routes/
├── services/
├── repositories/
├── models/
└── utils/
```

## 2. Standards

### 2.1 Naming Conventions
```kotlin
class UserRepository { }
fun getUserById(id: String): User?
val userName = "John"
const val MAX_RETRY_COUNT = 3
private val _users = MutableStateFlow<List<User>>(emptyList())
val users: StateFlow<List<User>> = _users.asStateFlow()
```

### 2.2 Null Safety
- ❌ **Bad:** `user!!.name`
- ✅ **Good:** `user?.name ?: "Unknown"` or `requireNotNull(user)`

### 2.3 Coroutines
- Use `viewModelScope` in Android.
- Use `coroutineScope` for parallel execution.
- Use `Flow` for reactive streams.

### 2.4 Data Classes & Immutability
- Use `data class` for models.
- Use `copy()` for updates.
- Use `sealed class` for UI state (Loading, Success, Error).

### 2.5 Extension Functions
- Use for utility logic (e.g., `String.isValidEmail()`).

### 2.6 Scope Functions
- Use `let`, `apply`, `also`, `run`, `with` appropriately.

### 2.7 Jetpack Compose
- Use `State` and `LaunchedEffect`.
- Separate UI from Logic (ViewModel).

### 2.8 Dependency Injection (Hilt)
- Use `@HiltViewModel`, `@Inject`, `@Module`, `@Provides`.

### 2.9 Error Handling
- Use `Result<T>` type.
- Handle exceptions in Repository/UseCase layer.

### 2.10 Performance
- Use `Sequence` for large collections.
- Use `LazyColumn` with keys.
- Use `remember` for expensive computations.

### 2.11 Testing
- Unit test ViewModels (`runTest`).
- Compose UI tests (`composeTestRule`).

### 2.12 Ktor Backend
- Configure Routing, Serialization, StatusPages.

### 2.13 Multiplatform
- Use `expect`/`actual` mechanism.

### 2.14 Code Style
- No semicolons.
- Expression body for simple functions.
- Trailing commas.

## 3. Prohibited Patterns
- ❌ `!!` operator (unless 100% certain).
- ❌ Overuse of `lateinit var`.
- ❌ Global variables.
- ❌ Magic numbers.
