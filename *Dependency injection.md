## iOS Developers Interview Dependency injection Questions

### 1. What is dependance injection? 
  - Dependency injection is a technique in which an object receives other objects that it depends on.
    
### 2. How many types of dependance injection?
  - `initializer injection`
```swift
      // Define a protocol for a service
  protocol DataService {
    func fetchData() -> String
  }

  // Implement the protocol
class NetworkService: DataService {
    func fetchData() -> String {
        return "Data from network"
    }
}

// Class that depends on the DataService
class DataManager {
    private let service: DataService
    
    // Initializer injection: Inject the dependency via the initializer
    init(service: DataService) {
        self.service = service
    }
    
    func getData() -> String {
        return service.fetchData()
    }
}

// Usage
let networkService = NetworkService()
let dataManager = DataManager(service: networkService)
print(dataManager.getData()) // Output: Data from network
```

  - `property injection`
 ```swift
// Define a protocol for a service
protocol LoggerService {
    func log(message: String)
}

// Implement the protocol
class ConsoleLogger: LoggerService {
    func log(message: String) {
        print("Log: \(message)")
    }
}

// Class that optionally depends on the LoggerService
class AnalyticsManager {
    // Property injection: The dependency is injected through a property
    var logger: LoggerService?
    
    func trackEvent(name: String) {
        logger?.log(message: "Event tracked: \(name)")
    }
}

// Usage
let consoleLogger = ConsoleLogger()
let analyticsManager = AnalyticsManager()

// Inject the dependency via property
analyticsManager.logger = consoleLogger
analyticsManager.trackEvent(name: "User SignUp") // Output: Log: Event tracked: User SignUp
```
  - `method injection`
```swift
    // Define a protocol for a database service
protocol DatabaseService {
    func saveData(_ data: String)
}

// Implement the protocol
class LocalDatabaseService: DatabaseService {
    func saveData(_ data: String) {
        print("Data saved: \(data)")
    }
}

// Class that uses a DatabaseService only in a specific method
class UserManager {
    func saveUserData(data: String, using service: DatabaseService) {
        // Method injection: Dependency is passed via method parameters
        service.saveData(data)
    }
}

// Usage
let databaseService = LocalDatabaseService()
let userManager = UserManager()

// Inject the dependency via method
userManager.saveUserData(data: "User info", using: databaseService) // Output: Data saved: User info
```
### 3. Advantages and disadvantages of dependency injection in swift.
  - Advantages of Dependency Injection in Swift
      - `Loose Coupling:` Dependency injection (DI) promotes loose coupling between classes. Instead of hardcoding dependencies within a class, you inject them externally, making it easier to swap out implementations without altering the class itself.

      - `Improved Testability:` With DI, you can pass mock or stub objects during testing, allowing for more precise unit tests. This helps in isolating individual units of code and ensuring they behave correctly without relying on actual dependencies.
        
   - Disadvantages of Dependency Injection in Swift
      - `Increased Complexity:` While DI simplifies the relationships between objects, it can introduce complexity in how dependencies are managed and injected. Beginners may find it difficult to grasp at first, and excessive use can lead to over-engineering.
      - `Difficult to Debug:` If you rely heavily on DI frameworks or complex DI setups, debugging can become harder, especially if the injection mechanism fails silently or if there are issues with configuration that manifest at runtime.

### 4. What is Tight Coupling and Loose Coupling?
   - `Tight Coupling`: Tight Coupling means one class is dependent on another class.
   - `Loose Coupling`: Loose Coupling means one class is dependent on interface rather than class.

### 5. What is Swinject?
  - Swinject is a lightweight and flexible dependency injection framework for Swift. It provides a way to manage the dependencies between objects, making your code more modular and easier to test. By using Swinject, you can decouple components in your application, leading to cleaner and more maintainable code
