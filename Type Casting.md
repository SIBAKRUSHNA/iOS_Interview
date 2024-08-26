## iOS Developers Interview Type Casting Questions

### 1. What is type casting in swift?
  - type casting is a way to check and convert from one type to another.

### 2. How many types of  type casting in swift?

- `Optional Casting (as?)`
     - This attempts to cast an object to a specific type and returns an optional

```swift
let someObject: Any = "Hello"
if let string = someObject as? String {
    print("It's a string: \(string)")
} else {
    print("It's not a string")
}
```

- `Forced Casting (as!)`
     - This attempts to cast an object to a specific type and forcibly unpacks the result. If the cast fails, a runtime error occurs.
       
```swift
let someObject: Any = "Hello"
let string = someObject as! String
print("It's a string: \(string)")
```
       
- `Type Conversion (as)`
     - This is used for converting between different types, especially in class hierarchies or when dealing with protocols.

```swift
let optionalNumber: Int? = 3
things.append(optionalNumber)        // Warning
things.append(optionalNumber as Any) // No warning
```
