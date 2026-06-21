
# iOS Unit Testing Interview Notes
<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 09_13_28 PM" src="https://github.com/user-attachments/assets/4faf3add-ec2d-4afc-8bd5-f8da2230238c" />

## 1. What is XCTest?

`XCTest` is Apple's official testing framework used for:

- Unit Testing
- UI Testing
- Performance Testing

```swift
import XCTest

class CalculatorTests: XCTestCase {

    func testAddition() {
        XCTAssertEqual(2 + 3, 5)
    }
}
```

---

## 2. What is Unit Testing?

Unit Testing verifies that a small piece of code (function, method, class) works correctly in isolation.

### Benefits

- Finds bugs early
- Improves code quality
- Enables safe refactoring
- Acts as documentation

```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func testAdd() {
    XCTAssertEqual(add(2, 3), 5)
}
```

---

## 3. Unit Test vs UI Test

| Unit Test | UI Test |
|------------|----------|
| Tests business logic | Tests user interaction |
| Fast | Slower |
| Runs in isolation | Runs on actual app |
| Uses mocks/stubs | Uses real UI |
| XCTestCase | XCUITest |

---

## 4. What are Assertions?

Assertions verify expected outcomes.

### Common Assertions

```swift
XCTAssertTrue(isValid)

XCTAssertFalse(isLoading)

XCTAssertEqual(result, expected)

XCTAssertNotEqual(result, expected)

XCTAssertNil(value)

XCTAssertNotNil(value)

XCTAssertThrowsError(try function())
```

---

## 5. What is Mocking?

Mocking replaces real dependencies with fake implementations.

### Example

```swift
class MockAPIService: APIServiceProtocol {

    func fetchUsers(completion: @escaping ([User]) -> Void) {
        completion([])
    }
}
```

### Benefits

- Fast tests
- No network dependency
- Predictable results

---

## 6. What is Dependency Injection?

Passing dependencies from outside instead of creating them internally.

```swift
class UserViewModel {

    private let service: UserServiceProtocol

    init(service: UserServiceProtocol) {
        self.service = service
    }
}
```

### Benefits

- Loose coupling
- Easier testing
- Supports mocking

---

## 7. How do you test asynchronous code?

Using `XCTestExpectation`.

```swift
func testFetchUsers() {

    let expectation = expectation(description: "Users fetched")

    service.fetchUsers { users in
        XCTAssertFalse(users.isEmpty)
        expectation.fulfill()
    }

    waitForExpectations(timeout: 3)
}
```

---

## 8. What is XCTestExpectation?

An object that waits for asynchronous operations to finish before ending the test.

```swift
let expectation = expectation(description: "API Call")

expectation.fulfill()

waitForExpectations(timeout: 5)
```

### Common Use Cases

- API Calls
- Combine Publishers
- Async Tasks
- Background Operations

---

## 9. Mock vs Stub

| Mock | Stub |
|--------|--------|
| Verifies interactions | Returns predefined data |
| Behavior Testing | State Testing |
| Tracks method calls | Supplies fake responses |

### Stub Example

```swift
class UserServiceStub: UserServiceProtocol {

    func fetchUsers(completion: @escaping ([User]) -> Void) {
        completion([User(name: "John")])
    }
}
```

### Mock Example

```swift
class UserServiceMock: UserServiceProtocol {

    var fetchCalled = false

    func fetchUsers(completion: @escaping ([User]) -> Void) {
        fetchCalled = true
        completion([])
    }
}
```

---

## 10. What are Test Doubles?

A generic term for fake objects used during testing.

### Types

### Dummy
Used only to satisfy parameters.

### Stub
Returns predefined data.

### Mock
Verifies interactions.

### Spy
Records method calls.

### Fake
Simplified working implementation.

---

## 11. What is Code Coverage?

Code Coverage measures how much code executes while running tests.

Example:

```text
80% Code Coverage
```

### Important

High coverage does NOT guarantee high-quality tests.

---

## 12. Why avoid real API calls in Unit Tests?

### Problems

- Slow execution
- Internet dependency
- Unstable results
- Third-party failures

### Preferred

Use mocks or stubs instead.

```swift
MockAPIService()
```

---

## 13. What are setUp() and tearDown()?

Used to prepare and clean test environments.

```swift
class UserTests: XCTestCase {

    var viewModel: UserViewModel!

    override func setUp() {
        super.setUp()
        viewModel = UserViewModel()
    }

    override func tearDown() {
        viewModel = nil
        super.tearDown()
    }
}
```

### Lifecycle

- `setUp()` → Before every test
- `tearDown()` → After every test

---

## 14. How do you test ViewModels?

Inject mocked services and verify outputs.

```swift
func testLoadUsers() {

    let mockService = MockUserService()

    let vm = UserViewModel(service: mockService)

    vm.loadUsers()

    XCTAssertEqual(vm.users.count, 2)
}
```

---

## 15. FIRST Principles

### F — Fast

Tests should execute quickly.

### I — Independent

Tests should not depend on each other.

### R — Repeatable

Tests should produce the same result every run.

### S — Self-Validating

Tests should automatically pass or fail.

### T — Timely

Tests should be written alongside production code.

---

# Additional Important Interview Questions

## 16. What is Test-Driven Development (TDD)?

A development approach where tests are written before implementation.

### TDD Cycle

```text
Red → Green → Refactor
```

1. Write failing test
2. Make test pass
3. Refactor code

---

## 17. State Testing vs Behavior Testing

### State Testing

Verifies output/state.

```swift
XCTAssertEqual(vm.users.count, 2)
```

### Behavior Testing

Verifies interactions.

```swift
XCTAssertTrue(mockService.fetchCalled)
```

---

## 18. What is @testable import?

Allows tests to access `internal` members.

```swift
@testable import MyApp
```

Useful for testing:

```swift
internal class UserManager { }
```

---

## 19. How do you test throwing functions?

```swift
func testLoginThrowsError() {

    XCTAssertThrowsError(
        try authService.login()
    )
}
```

---

## 20. How do you test async/await code?

```swift
func testFetchUsers() async throws {

    let users = try await service.fetchUsers()

    XCTAssertEqual(users.count, 2)
}
```

---

## 21. What is a Spy Object?

Records interactions for later verification.

```swift
class AnalyticsSpy {

    var eventTracked = false

    func trackEvent() {
        eventTracked = true
    }
}
```

---

## 22. How do you test Combine Publishers?

```swift
func testPublisher() {

    let expectation = expectation(description: "Receive value")

    let cancellable = publisher.sink { value in
        XCTAssertEqual(value, "Hello")
        expectation.fulfill()
    }

    waitForExpectations(timeout: 1)
}
```

---

## 23. What is Performance Testing?

Measures execution speed.

```swift
func testPerformanceExample() {

    measure {
        _ = largeDataProcessing()
    }
}
```

---

## 24. What is a Flaky Test?

A test that passes sometimes and fails sometimes.

### Causes

- Network dependency
- Timing issues
- Shared state
- Concurrency problems

---

## 25. What should be Unit Tested?

### Test These

✅ Business Logic  
✅ ViewModels  
✅ Utility Classes  
✅ Validation Logic  
✅ Data Mapping

### Avoid

❌ Real API Calls  
❌ Database Calls  
❌ Third-Party Services  
❌ UIKit Screens

---

## 26. Testing MVVM Architecture

```text
View
 ↓
ViewModel ← Unit Test Here
 ↓
Service (Mock)
```

Most tests focus on:

- ViewModel
- Use Cases
- Repositories
- Services

---

## 27. Dependency Inversion Principle

High-level modules should depend on abstractions, not concrete implementations.

```swift
protocol APIServiceProtocol { }

class APIService: APIServiceProtocol { }
```

### Benefit

Makes mocking and testing easier.

---

## 28. What is Branch Coverage?

Measures whether every decision path is tested.

```swift
if isPremium {
    showPremiumScreen()
} else {
    showFreeScreen()
}
```

Test both branches.

---

## 29. Arrange – Act – Assert (AAA)

A standard test structure.

```swift
func testLogin() {

    // Arrange
    let vm = LoginViewModel()

    // Act
    vm.login()

    // Assert
    XCTAssertTrue(vm.isLoggedIn)
}
```

---

## 30. Characteristics of a Good Unit Test

- Fast
- Independent
- Repeatable
- Readable
- Deterministic
- Maintainable

### Good Naming Convention

```swift
func testLogin_WhenCredentialsAreValid_ShouldReturnSuccess()
```

This naming pattern is commonly expected in senior iOS interviews.

---

# Quick Interview Revision

### Core Topics

- XCTest
- XCTestCase
- Assertions
- Mocking
- Stubbing
- Dependency Injection
- Test Doubles
- Async Testing
- XCTestExpectation
- Code Coverage
- TDD
- MVVM Testing
- Combine Testing
- Performance Testing
- FIRST Principles
- AAA Pattern
- @testable import
- Async/Await Testing
