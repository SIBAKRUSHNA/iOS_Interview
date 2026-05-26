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

### 8. Optional Methods in Protocols – Swift Notes
  ## 1. Optional Methods Using @objc
   - Swift protocols support optional methods only with @objc.
``` swift
@objc protocol Vehicle {

    func start()

    @objc optional func stop()
}
```
- Conforming Class
``` swift
class Car: Vehicle {

    func start() {
        print("Start")
    }

    // stop() is optional
}
```
- Calling Optional Method
``` swift
let car = Car()

car.stop?()
```
- Important Points
   - Optional methods require @objc
   - Works only with classes
   - Uses Objective-C runtime
   - Optional method must be called using ?
- Real UIKit Examples
   - UITableViewDelegate
   - UIScrollViewDelegate
 
 ## 2. Modern Swift Preferred Approach
  - Instead of optional methods, Swift prefers default implementation using protocol extensions.
``` swift
Protocol
protocol Downloadable {

    func startDownload()

    func cancelDownload()
}
```
- Default Implementation
``` swift
extension Downloadable {

    func cancelDownload() {
        print("Default cancel")
    }
}
```
- Conforming Type
``` swift
class FileDownloader: Downloadable {

    func startDownload() {
        print("Downloading...")
    }

    // cancelDownload() becomes optional
}
```
- Usage
``` swift
let file = FileDownloader()

file.startDownload()
file.cancelDownload()
```
- Output
``` swift
Downloading...
Default cancel
```
