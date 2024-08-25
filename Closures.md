## iOS Developers Interview Closures Questions

### 1. what is closure in swift?
  - Closures are self-contained blocks of functionality that can be passed around and used in your code.
    
    `Example of a Closure`
    ```swift
    let sumClosure = { (a: Int, b: Int) -> Int in
    return a + b
    }
    
    let result = sumClosure(3, 5)
    ```

### 2. How many types of closure?
`Auto closure`
    - An autoclosure is a closure that is automatically created to wrap an expression that’s passed as an argument to a 
      function.
  ```swift
           func logIfTrue(_ predicate: @autoclosure () -> Bool) {
                if predicate() {
                print("True")
              }
           }
   logIfTrue(3 > 2)  // prints "True"
  ```
`Trailing closure`
    - Trailing closure is a syntactic convenience that allows you to write a closure expression outside of a function's parentheses when the closure is the last argument of the function.
```swift
    func performOperation(_ a: Int, _ b: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(a, b)
}

  // Using a normal closure syntax
   let result = performOperation(3, 5, operation: { (a, b) in
    return a + b
    })

   // Using trailing closure syntax
    let resultWithTrailingClosure = performOperation(3, 5) { (a, b) in
       return a + b
   }

  print(result)  // 8
  print(resultWithTrailingClosure)  // 8
```
`Capture value`
    - In Swift, capturing values refers to a closure’s ability to capture and store references to constants and variables from the surrounding context in which it is defined.
    
```swift
      func makeIncrementer(incrementAmount: Int) -> () -> Int {
    var total = 0
    let incrementer: () -> Int = {
        total += incrementAmount
        return total
    }
    return incrementer
}

let incrementByTwo = makeIncrementer(incrementAmount: 2)

print(incrementByTwo())  // 2
print(incrementByTwo())  // 4
print(incrementByTwo())  // 6
```
`Escaping closure`
     - Closures passed as arguments to a function can be marked with @escaping if they need to escape the scope of the 
       function.
```swift
 var storedClosure: (() -> Void)?

func performTask(completion: @escaping () -> Void) {
    // Store the closure for later use
    storedClosure = completion
    print("Task started")
}

// Call the function and pass a closure
performTask {
    print("Task completed!")
}

// The closure hasn't been called yet
print("Task is still running...")

// Call the stored closure manually later
storedClosure?()
```
`Non escaping closure`
    - A non-escaping closure in Swift is a closure that is guaranteed to be executed before the function it is passed to 
      returns.
```swift
func performOperation(completion: () -> Void) {
    print("Operation started")
    // Execute the closure immediately within the function
    completion()
    print("Operation completed")
}

// Call the function and pass a closure
performOperation {
    print("Closure executed")
}
```
### 3. Closures are value type or reference type?
  - Closures are reference types.
