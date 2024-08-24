

### 1. What is the use and working process of try an try? and try! ?
 `try:`
  - Purpose: Used when you want to handle errors explicitly.
  - How it works: You wrap the code in a do-catch block. If an error is thrown, it will be caught in the catch block.
```swift
do {
    let result = try someFunctionThatThrows()
} catch {
    // Handle the error
}
```
`try?:`

  - Purpose: Converts the result into an optional (nil if there's an error, or a value if successful).
  - How it works: If the function throws an error, you get nil instead of an error.

```swift
let result = try? someFunctionThatThrows()
```

`try!:`
  - Purpose: Force-unwraps the result, assuming no error will be thrown.
  - How it works: If the function does throw an error, your app will crash.

```swift
let result = try! someFunctionThatThrows()
```
