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
