## iOS Developers Interview Macro Questions
### 1. # Swift Macros – Interview Notes

### What is a Macro?

A macro in Swift is a compile-time code generation feature introduced in Swift 5.9.

It automatically generates Swift code during compilation to reduce boilerplate and improve code readability.

---

### Why Use Macros?

* Reduce repetitive code
* Generate boilerplate automatically
* Safer metaprogramming
* Improve maintainability
* Compiler-supported code generation

---

### Macro Categories

Swift macros are divided into 2 categories:

1. Freestanding Macros
2. Attached Macros

---

## 1. Freestanding Macros

Used independently with `#`.

Example:

```swift
#stringify(a + b)
```

## Types

### a) Expression Macro

Returns an expression.

Example:

```swift
let result = #stringify(2 + 3)
```

Generated:

```swift
(5, "2 + 3")
```

---

### b) Declaration Macro

Generates declarations.

Example:

```swift
#generateMock(APIService)
```

May generate:

```swift
class MockAPIService: APIService { }
```

---

## 2. Attached Macros

Used with `@`.

Example:

```swift
@Observable
class UserViewModel { }
```

---

# Types of Attached Macros

## a) Peer Macro

Adds declarations beside original code.

Example:

```swift
@Mockable
protocol APIService { }
```

Generated:

```swift
class MockAPIService: APIService { }
```

---

## b) Member Macro

Adds members inside a type.

Example:

```swift
@AddInit
struct User {
    var name: String
}
```

Generated:

```swift
init(name: String) {
    self.name = name
}
```

---

## c) Accessor Macro

Adds getter/setter.

Example:

```swift
@UserDefault("username")
var username: String
```

Generated:

```swift
get { ... }
set { ... }
```

---

## d) Member Attribute Macro

Adds attributes to members automatically.

Used in:

```swift
@Observable
```

---

## e) Conformance Macro

Adds protocol conformance.

Example:

```swift
@Codable
struct User { }
```

Generated:

```swift
extension User: Codable { }
```

---

# Real SwiftUI Example

Without macro:

```swift
class UserViewModel: ObservableObject {
    @Published var name = ""
}
```

With macro:

```swift
@Observable
class UserViewModel {
    var name = ""
}
```

Macro automatically generates observation code.

---

# Macro Syntax

## Freestanding

```swift
#macroName()
```

## Attached

```swift
@MacroName
```

---

# Advantages

* Less boilerplate
* Compile-time safety
* Cleaner code
* Better maintainability
* Type-safe code generation

---

# Macro vs Property Wrapper

| Property Wrapper  | Macro                  |
| ----------------- | ---------------------- |
| Runtime feature   | Compile-time feature   |
| Limited scope     | Can generate full code |
| Example: `@State` | Example: `@Observable` |

---

# Important Interview Points

* Introduced in Swift 5.9
* Works at compile time
* Uses SwiftSyntax and compiler plugins
* Generates Swift code automatically
* Helps reduce repetitive code

---

# Interview One-Line Answer

“Macros in Swift are compile-time code generation tools that automatically generate Swift code to reduce boilerplate and improve maintainability.”
