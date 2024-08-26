## iOS Developers Interview Protocols Questions

### 1. What is protocol in swift?
  - A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task.

```swift
// Define a protocol
protocol Drivable {
    var isEngineRunning: Bool { get set }
    func startEngine()
    func stopEngine()
}

// Conform to the protocol with a class
class Car: Drivable {
    var isEngineRunning: Bool = false
    
    func startEngine() {
        isEngineRunning = true
        print("Engine started")
    }
    
    func stopEngine() {
        isEngineRunning = false
        print("Engine stopped")
    }
}

// Usage
let myCar = Car()
myCar.startEngine()  // Output: Engine started
myCar.stopEngine()   // Output: Engine stopped
```

### 2. What is protocol extension?
  - Protocols can be extended to provide method, initializer, subscript, and computed property implementations to conforming types.

### 3. What is Protocol Inheritance?
  - Protocols can inherit from other protocols in a similar way to classes inheriting from superclasses.

### 4. What is Protocol Composition?
  - It is the process of combining multiple protocol into a single protocol.

### 5. Can we declare variable in protocol?
  - Yes, It must be var and it must be read-Only or readAndWrite.

### 6. Can we declare an optional protocol method in swift?
  - Yes. In that protocol name and optional methods should be followed by @objc due to it consider as objective c code.
    
``` swift
// Define a protocol with an optional method
@objc protocol Responder {
    @objc optional func respondToAlert()
}

// Create a class that conforms to the protocol and implements the optional method
class FireAlarm: NSObject, Responder {
    func respondToAlert() {
        print("FireAlarm: Responding to fire alert!")
    }
}

// Create another class that conforms to the protocol but does not implement the optional method
class SecurityAlarm: NSObject, Responder {
    // No implementation for respondToAlert
}
```

### 7. Can protocol be fileprivate?
  - Yes. Protocol can be fileprivate, private, public. Private and fileprivate protocol can be confirmed only within current file.
