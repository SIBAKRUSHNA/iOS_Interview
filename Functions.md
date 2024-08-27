## iOS Developers Interview Functions Questions

### 1. What inout function parameters in swift?
  - In Swift, function parameters are constants by default. This means that the values of the parameters passed to a function cannot be modified within the function. However, there may be cases where you want to modify the values of the parameters passed to a function. This is where inout parameters come in.

```swift
func increment(_ value: inout Int) {
    value += 1
}

var number = 10
increment(&number)
print(number)  // Output: 11
```

### 2. What is difference between function and method?
  - A method is a function that is associated with a type, that is, a class, a struct, or an enum. This means that every method is a function, but not every function is a method.
