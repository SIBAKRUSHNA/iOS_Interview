## iOS Developers Interview Access Control Questions

### 1. What are the access controls in swift?
  - open
  - public
  - internal
  - private
  - fileprivate

### 2. What is the open access controls?
  - Access to data members and member functions not only within the same module or target but also outside of it.
    
### 3. What is the public access controls?
  - Accessed from any module, but they subclassed or overridden with the module.
   
### 4. What is the internal access controls?
  - Accessed, subclassed or overridden with the module.
### 5. What is the private access controls?
  - Accessed, subclassed or overridden with the scope.
### 6. What is the fileprivate access controls?
  - Accessed, subclassed or overridden with the swift file.
### 7. How to implement a property which is public/internal but mutation is private?
- In Swift, you can use the `private(set)` keyword to make a property's setter private, and the `public` keyword to make its getter public.
  
```swift
class Student {
     var name: String
     private(set) public var age: Int
     init(name: String, age: Int) {
         self.name = name
         self.age = age
     }
 }
 let robert = Student(name: "Robert Martin", age: 15)
 // accessible because of the public getter
 print(robert.age) // print: 15
 // assigning or changing a value is not allowed
```
### 8. Can you use the private properties in extensions?
  - Yes, if extension is present in same swift file.
    
