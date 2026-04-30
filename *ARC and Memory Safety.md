## iOS Developers Interview ARC and Memory Safety Questions

### 1. What is arc in swift?
   - ARC is Swift’s memory management system that automatically tracks and manages the lifecycle of class instances. It works by keeping a reference count for each object.

      - When you create an object → reference count = 1
      - When you assign it to another variable → count increases
      - When a reference is removed → count decreases
      - When the count becomes 0 → the object is deallocated (memory freed)
     
### 2.  How arc decide that this object not need long time ios swift?
   - It determines an object's lifetime by keeping track of its reference counts. ARC is mainly driven by the Swift compiler which inserts retain and release operations. At runtime, retain increments the reference count and release decrements it. When the reference count drops to zero, the object will be deallocated.
    <img width="996" height="1015" alt="ChatGPT Image Apr 30, 2026, 08_39_18 PM" src="https://github.com/user-attachments/assets/9f385642-c727-4cc8-86a0-0bde26004254" />


### 3. What is zombie object in swift ?
   - A Zombie Object is an instance that has already been deallocated from memory by ARC (Automatic Reference Counting), but your code still holds a reference to it and tries to use it. When this happens, the app crashes with errors like:
     - EXC_BAD_ACCESS
 -  🔍 Why it happens
     - ARC frees an object when its strong reference count becomes 0
     - But if you still have a dangling reference (e.g., weak or unowned)
     - And you try to access that object → 💥 crash

### 4. What is Strong Reference ?
   - A Strong Reference in Swift is a reference that keeps an object alive in memory by increasing its reference count under Automatic Reference Counting (ARC).
   - 🔍 Explanation
        - By default, all references in Swift are strong
        - When you assign an object to a variable/property → its reference count increases
        - The object is not deallocated as long as at least one strong reference exists

### 5. What is weak Reference ?
   - A weak reference in Swift is a reference that does NOT increase the object’s reference count, meaning it doesn’t keep the object alive in memory.
   - 🔍 Explanation
       - Declared using weak
       - Always an optional (?)
       - Automatically becomes nil when the referenced object is deallocated
       - Used to avoid retain cycles (memory leaks)
     
### 6. What is unowned Reference ?
   -  An unowned reference in Swift is a non-owning reference that does NOT increase the reference count, but assumes the referenced object will always exist while it’s being used.
   -  🔍 Explanation
       - Declared using unowned
       - Does not retain the object (like weak)
       - Does NOT become nil automatically
       - Used when the referenced object has the same or longer lifetime
       - If accessed after deallocation → 💥 runtime crash (EXC_BAD_ACCESS)

### 7. What is the difference between weak and unowned reference?
  - Weak references are always optional and unowned references are always non-optional.
  - Weak references are safer as they automatically become nil when the object is deallocated. Unowned references 
    can cause crashes if the object is deallocated.
  - 📌 When to use what?
   - Use weak
     - Delegates (weak var delegate)
     - When lifecycle is uncertain
     - Safer default choice
   - Use unowned
     - When two objects have same lifetime
     - When nil is logically impossible
     - Example: child → parent relationship
```swift
import Foundation

class Owner {
    var child: Child?

    func createChild() {
        child = Child(owner: self)
    }
}

class Child {
    unowned var owner: Owner

    init(owner: Owner) {
        self.owner = owner
    }

    func doSomething() {
        print("Owner's reference is \(owner)")
    }
}

func testUnownedReference() {
    var owner: Owner? = Owner()
    owner?.createChild()

    // Access the child and perform an operation
    owner?.child?.doSomething()

    // Now deallocate the owner
    owner = nil

    // The owner has been deallocated, but the child still has an unowned reference to it.
    // Trying to access the owner through the child will now cause a crash.
    // Uncomment the following line to see the crash:
    // owner?.child?.doSomething()
}

testUnownedReference()
```
### 8. what is retain cycle?
   - A retain cycle (also called a strong reference cycle) happens when two or more objects hold strong references to each other, so their reference counts never reach zero and ARC cannot deallocate them, causing a memory leak.
   - 🔍 Why it happens
        - Swift uses Automatic Reference Counting (ARC)
        - Objects are deallocated only when strong reference count = 0
        - If objects strongly reference each other, the count never becomes 0
          
   - ⚠️ Real-world scenario (very common)
       - Closures capturing self strongly
       - Delegate pattern without weak
       - Parent-child objects referencing each other strongly
     
### Retain Cycle Example
``` swift
class Parent {
    var child: Child?
    
    deinit {
        print("Parent is being deinitialized")
    }
}
class Child {
    var parent: Parent?
    
    deinit {
        print("Child is being deinitialized")
    }
}
var parentInstance: Parent? = Parent()
var childInstance: Child? = Child()

parentInstance?.child = childInstance
childInstance?.parent = parentInstance

parentInstance = nil
childInstance = nil

```
![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*6ckwxMS823wjVZFpMfk6jg.png)

### Resolving the Retain Cycle
``` swift
class Parent {
    var child: Child?
    
    deinit {
        print("Parent is being deinitialized")
    }
}
class Child {
    weak var parent: Parent?  // Use weak to avoid retain cycle
    
    deinit {
        print("Child is being deinitialized")
    }
}
var parentInstance: Parent? = Parent()
var childInstance: Child? = Child()

parentInstance?.child = childInstance
childInstance?.parent = parentInstance

parentInstance = nil
childInstance = nil

```    
![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*A6yTWls7nfluyhS1R_ypBA.png)
