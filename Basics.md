   ##                                              iOS Developers Interview Basics Questions
### 1. What’s the difference between var and let? Which one would you choose for properties in a struct and why?
  - var is used to declare variables whose values can change after they are initially set. You can reassign a new value to a var property.
  - let is used to declare constants whose values cannot change once they are assigned. Once a value is set for a let property, it cannot be 
             modified.
   ###                            Choosing Between var and let for Properties in a Struct
   -> In general, prefer let wherever possible to make your code safer and only use var when you need to allow changes to the property.

### 2.
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
     
### 3. what is  typealias in swift ?
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

### 4.

### 5.

### 6.

### 7.

### 8.

### 9.

### 10.
