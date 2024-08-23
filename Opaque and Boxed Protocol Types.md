## iOS Developers Interview Opaque and Boxed Protocol Types Questions

### 1. What is box protocol in swift ?
-  In Swift, a boxed protocol type can store any type that conforms to a given protocol, but the type isn't known until 
   runtime.

 ```swift
   protocol Animal {
    func sound() -> String
}

struct Dog: Animal {
    func sound() -> String {
        return "Woof!"
    }
}

struct Cat: Animal {
    func sound() -> String {
        return "Meow!"
    }
}

class AnimalBox<T: Animal>: Animal {
    var value: T
    init(_ value: T) {
        self.value = value
    }
    func sound() -> String {
        return value.sound()
    }
}
let dog = Dog()
let cat = Cat()

let boxedDog = AnimalBox(dog)
let boxedCat = AnimalBox(cat)

var animals: [Animal] = [boxedDog, boxedCat]

for item in animals {
    print(item.sound())
}
```
### 2. What is opaque types in swift?
  - Opaque type refers to a type that complies with a particular protocol but keeps the actual type hidden.

    ```swift
    protocol Calcualte {
    func getValue() -> Int
    }
    
    struct Add: Calcualte {
    var valueOne = 0
    var valueTwo = 0
    func getValue() -> Int {
       return valueOne + valueTwo
       }
     }

    func getResult() -> some Calcualte {
      return Add(valueOne: 20, valueTwo: 30)
    }
    let value = getResult()
    print(value.getValue())
    ```
