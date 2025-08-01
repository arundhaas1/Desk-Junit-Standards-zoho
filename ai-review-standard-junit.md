
# 🧪 Java Unit Test Review Standards

Follow these essential standards for writing clean, reliable, and maintainable unit tests in Java.

---

### 1. ✅ Avoid lenient argument matchers  
Do **not** use the following Mockito matchers:
- `any()`
- `anyObject()`
- `anyString()`
- `anyInt()`
- `anyLong()`
- `anyDouble()`
- `anyFloat()`
- `anyBoolean()`
- `anyByte()`
- `anyShort()`
- `anyChar()`
- `anyList()`
- `anySet()`
- `anyMap()`
- `anyCollection()`
- `any(Class.class)`

These matchers make tests too generic and reduce assertion accuracy. Always use exact or descriptive arguments.

---

### 2. ❌ Avoid usage of `spy()`  
Avoid using `Mockito.spy()` as it leads to fragile and hard-to-maintain tests.  
Favor proper mocking using `@Mock` and clean architecture over spying real objects.

---

### 3. 📛 Follow `given_when_then` naming convention  
Use descriptive and structured names like:
```
givenValidRequest_whenSave_thenReturnsSuccess()
```
This improves test readability and quickly communicates the test scenario.

---

### 4. 🏷️ Use `@DisplayName` annotation  
Annotate each test with `@DisplayName`:
```java
@DisplayName("Should return error for invalid token")
@Test
void givenInvalidToken_whenGetData_thenThrowException() {
    ...
}
```
This enhances test reporting and improves readability for reviewers.

---

### 5. 💉 Use `@Mock` and `@InjectMocks`  
Always:
- Use `@Mock` for dependencies
- Use `@InjectMocks` for the class under test

Avoid manual constructor injection with `new ...`, unless absolutely required.

---

### 6. 🔒 Use `assertAll()` for multiple assertions  
Wrap multiple assertions like this:
```java
assertAll(
    () -> assertEquals(200, response.getCode()),
    () -> assertEquals("OK", response.getMessage())
);
```
This ensures all checks are run and failure messages are informative.

---

### 7. 📦 Move constants to a separate class  
Do not hardcode values like `"active"`, `500L`, `"error"` in your test methods.  
Extract them into a `TestConstants` class to improve maintainability and reuse.

---

### 8. 🔁 Prefer `when(...).thenReturn(...)` over `doReturn(...).when(...)`  
✅ Preferred:
```java
when(service.getStatus()).thenReturn("active");
```

🚫 Avoid:
```java
doReturn("active").when(service).getStatus();
```

Only use `doReturn()` in rare edge cases like spying or final methods.

---

### 9. 📋 Other basic best practices  
- Keep each test focused on **one behavior**  
- Do not assert directly on mocks  
- Avoid `Thread.sleep()` or arbitrary delays  
- Clearly separate **Arrange → Act → Assert** sections  
- Mock only external dependencies — not internal logic  
- Keep setup logic minimal and relevant  
- Prefer meaningful test data and method names

---

🧩 Adhering to these standards ensures your test suite is clear, robust, and easy to evolve.
