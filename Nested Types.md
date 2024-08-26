## iOS Developers Interview Nested Types Questions

### 1. What is nested type in swift?
  - Define type inside scope of another type.
```swift
struct Car {
    var make: String
    var model: String
    
    enum CarType {
        case sedan, coupe, convertible, suv
    }
    var type: CarType
}
let myCar = Car(make: "Toyota", model: "Camry", type: .sedan)
print("My car is a \(myCar.make) \(myCar.model) which is a \(myCar.type).")
```
