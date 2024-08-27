## iOS Developers Interview Generics Questions

### 1. What is generics?
  - Generic code enables you to write flexible, reusable functions and types that can work with any type, subject to requirements that you define.

```swift
func swapValues<T>(a: inout T, b: inout T) {
    let temp = a
    a = b
    b = temp
}

var x = 5
var y = 10
swapValues(a: &x, b: &y)
print("x: \(x), y: \(y)")  // Output: x: 10, y: 5
```
