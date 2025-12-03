# Java Language Rules

## 1. Spring Boot Standards
- ✅ **Lombok:** Use Lombok to reduce boilerplate.
- ✅ **Architecture:** Layered (Controller → Service → Repository).
- ✅ **Bean Validation:**
  ```java
  public class UserDTO {
      @NotNull
      @Email
      private String email;
      
      @Min(18)
      @Max(120)
      private int age;
  }
  ```

## 2. Error Handling
- Handle exceptions at the appropriate layer.
- Use Global Exception Handler (`@ControllerAdvice`).
