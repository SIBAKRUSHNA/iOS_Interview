## iOS Developers Interview Optional and Optional Chaining Questions

### 1. What is optional in swift?
  - An optional in Swift is basically a constant or variable that can hold a value OR nil.

### 2. 

### 3. What is difference between guard let and if let in swift?
  - guard let you are creating a new variable that will exist in the current scope.
  - In if let, you can not access out the scope and also you do not need to return statement.
    
### 4. What is optional chaining?
  - Optional chaining is a process in which is used to call properties, methods and subscripts of an optional that might currently be nil.
    
### 5. Optional internal implementation.

```swift
enum Optional<Wrapped> {
    case none
    case some(Wrapped)
}
```
