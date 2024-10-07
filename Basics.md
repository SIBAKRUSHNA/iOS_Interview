   ## iOS Developers Interview Basics Questions
   
### 1. What’s the difference between var and let? Which one would you choose for properties in a struct and why?
  - var is used to declare variables whose values can change after they are initially set. You can reassign a new value to a var property.
  - let is used to declare constants whose values cannot change once they are assigned. Once a value is set for a let property, it cannot be 
             modified.
   ###                            Choosing Between var and let for Properties in a Struct
   -> In general, prefer let wherever possible to make your code safer and only use var when you need to allow changes to the property.

### 2. what is type annotation in swift?
   - type annotation is the process of explicitly specifying the type of a variable, constant, or function. While Swift can often infer types automatically 
     based on the value assigned, you can provide a type annotation to make the type explicit.

    
   ```swift
   // Variable with type annotation
     var message: String = "Hello, World!"
   // Constant with type annotation
     let year: Int = 2024
   // Function with type annotations
     func greet(name: String) -> String {
      return "Hello, \(name)!"
      }
   ```
     
### 3. what is  typealias in swift?
   - In Swift, a typealias is a feature that allows you to define an alternative name (or alias) for an existing type. This can be useful for making code 
     more readable, for simplifying complex type names, or for providing meaningful names that better describe the role of the type in your code.

```swift
  // Defining a typealias for a tuple
typealias HTTPStatus = (code: Int, message: String)

let success: HTTPStatus = (200, "OK")
let notFound: HTTPStatus = (404, "Not Found")

// Defining a typealias for a closure
typealias CompletionHandler = (Bool) -> Void

func loadData(completion: CompletionHandler) {
    // Some loading logic...
    completion(true)
}
   ```

### 4. what is tuple in swift?
   -  Tuple is a group of multiple values combined into a single compound value.

 ```swift
   func getUser() -> (name: String, age: Int) {
    return ("Alice", 30)
}

let user = getUser()
print(user.name)  // "Alice"
print(user.age)   // 30
 ```
### 5. What is self and Self in swift?
  - self :- self refers to the current instance, in the body of one of this method.
  - Self :- Self is used to refer to the type of the current class, structure, enumeration with its own method or 
    initializer.

### 6. What is defer keyword in Swift?
  - Defer is a keyword that declares a block of code that will only be expected when execution leaves the current scope.

### 7. What is mutating keyword in Swift?
  - The property of value type can not be modified within its instance method by default.

### 8. What is Any in swift?
  - Any can represent an instance of any type at all, including function types.

### 9. What is AnyObject in swift ?
  - AnyObject can represent an instance of any class type.

### 10. What is use of the static keyword in swift?
  - The Static keyword makes it easier to utilize an objects properties or methods without the need of managing instances. Use of the Static keyword in the Singleton pattern can reduce memory leaks by mismanaging instances of classes.

### 11. What is type inference in Swift?
  - Type inference allows you to declare a variable or constant without explicitly specifying its data type.

### 12. What is difference between static and dynamic library in in swift?
  - Static libraries provide simplicity, performance, and code protection.
  - While dynamic libraries offer code sharing, versioning flexibility, and dynamic loading capabilities.
    
### 13. What is the difference between Static and Class variable?
### 14. What is associativity in swift?
  - In Swift, associativity is the order in which operators of the same precedence are grouped together

### 15. What is Associated Types?
  - In Swift, associated types are a powerful feature used with protocols to define placeholder types that can be specified later by conforming types.

### 16. What is type safe in swift?
   - Type safety in Swift is a feature that ensures code is checked for type errors before it's compiled.
     
### 17. What is apple human interface guidelines(HIG)?
   - The HIG offers guidance and best practices for designing exceptional user experiences across all Apple platforms.
