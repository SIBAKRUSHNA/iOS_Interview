## iOS Developers Interview SOLID Principles Questions

### 1. SOLID Principles in Swift

 - `Single Responsibility Principle`
    - There should never be more than one reason for a class to be change.
```swift
class User {
    var name: String
    var email: String
    
    init(name: String, email: String) {
        self.name = name
        self.email = email
    }
}

class UserValidator {
    func isValidEmail(_ email: String) -> Bool {
        // Email validation logic
        return email.contains("@")
    }
}
```

 - `Open-Closed Principle`
    - Software entities (Class. Modules, Functions etc) should open for extension but close for modification. 
```swift
protocol Employee {
    func calculateSalary() -> Double
}

class FullTimeEmployee: Employee {
    func calculateSalary() -> Double {
        return 3000
    }
}

class PartTimeEmployee: Employee {
    func calculateSalary() -> Double {
        return 1500
    }
}

// Adding a new type of employee
class Intern: Employee {
    func calculateSalary() -> Double {
        return 800
    }
```

 - `Liskov Substitution Principle`
    - Function that use references to base class must be able to use objects of derived classes without knowing it.

```swift
// Define a base protocol for all payment methods
protocol PaymentMethod {
    func processPayment(amount: Double)
}

// Subclass for credit card payments, conforms to PaymentMethod
class CreditCard: PaymentMethod {
    func processPayment(amount: Double) {
        print("Processing credit card payment of $\(amount)")
    }
}

// Subclass for cash payments, conforms to PaymentMethod
class Cash: PaymentMethod {
    func processPayment(amount: Double) {
        print("Processing cash payment of $\(amount)")
    }
}

// Function that expects any payment method to process payment
func pay(bill: PaymentMethod, amount: Double) {
    bill.processPayment(amount: amount)
}

// Example usage
let creditCardPayment = CreditCard()
let cashPayment = Cash()

pay(bill: creditCardPayment, amount: 100.0)  // Output: "Processing credit card payment of $100.0"
pay(bill: cashPayment, amount: 50.0)         // Output: "Processing cash payment of $50.0"
```

 - `Interface Segregation Principle`
    - Client should not be forced to depend upon interfaces that they do not use.

```swift
protocol Runnable {
    func run()
}

protocol Flyable {
    func fly()
}

class DogISP: Runnable {
    func run() {
        print("Dog is running")
    }
}

class BirdISP: Runnable, Flyable {
    func run() {
        print("Bird is running")
    }
    
    func fly() {
        print("Bird is flying")
    }
}
```

 - `Dependency Inversion Principle`
    - High level modules should not depend upon low level modules. Both should depend upon abstractions.
    - Abstractions should not depend upon details. Details should depend upon abstractions.

```swift
```
