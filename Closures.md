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
`Escaping closure`
`Non escaping closure`

### 3. Closures are value type or reference type?
  - Closures are reference types.
    
### 4. 
