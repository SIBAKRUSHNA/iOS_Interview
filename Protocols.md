## iOS Developers Interview Protocols Questions

### 1. what is protocol in swift?
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
