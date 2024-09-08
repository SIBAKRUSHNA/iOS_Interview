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
### 3. What is Swinject?
  - Swinject is a lightweight and flexible dependency injection framework for Swift. It provides a way to manage the dependencies between objects, making your code more modular and easier to test. By using Swinject, you can decouple components in your application, leading to cleaner and more maintainable code
