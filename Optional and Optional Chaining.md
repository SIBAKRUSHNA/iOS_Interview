## iOS Developers Interview Optional and Optional Chaining Questions

### 1. What is optional in swift?
  - An optional in Swift is basically a constant or variable that can hold a value OR nil.

### 2. 

### 3. What is difference between guard let and if let in swift?
 ## if let
  - Used for optional checking
  - Executes code only when value exists
  - Variable scope is inside if block
 ```swift   
if let name = userName {
    print(name)
}
```
- Use When
  - Optional value is not mandatory
  - Need separate else handling
  - Small conditional checks

## guard let
  - Used for early exit
  - Value is required for remaining function
  - Avoids nested code
  - Variable available after guard statement
 ```swift 
guard let name = userName else {
    return
}

print(name)
```
 - Use When
   - Validation required
   - Clean readable code needed
   - Value mandatory for execution
    
### 4. What is optional chaining?
  - Optional chaining is a process in which is used to call properties, methods and subscripts of an optional that might currently be nil.
    
### 5. Optional internal implementation.

```swift
enum Optional<Wrapped> {
    case none
    case some(Wrapped)
}
```
