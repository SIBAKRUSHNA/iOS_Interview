## iOS Developers Interview ARC and Memory Safety Questions

### 1. What is arc in swift?
   - Automatic Reference Counting (ARC) to track and manage your app's memory usage.
     
### 2. - How arc decide that this object not need long time ios swift?
   - It determines an object's lifetime by keeping track of its reference counts. ARC is mainly driven by the Swift compiler which inserts retain and release operations. At runtime, retain increments the reference count and release decrements it. When the reference count drops to zero, the object will be deallocated.

### 3. What is zombie object in swift ?
   - Detection of Zombie Objects: When an object is deallocated from memory but still has a reference.

### 4. What is Strong Reference ?
   - Strong reference means object keep alive in the memory.

### 5. What is weak Reference ?
   - Weak reference means object doesn’t keep alive in the memory.
     
### 6. What is unowned Reference ?
   -  Unowned reference means object doesn’t keep alive in the memory.

### 7. What is the difference between weak and unowned reference?
  - Weak references are always optional and unowned references are always non-optional.
  - Weak references are safer as they automatically become nil when the object is released. Unowned references 
    can cause crashes if the object is destroyed
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
   - A retain cycle occurs in Swift when two or more objects hold strong references to each other, preventing 
     them from being deallocated.
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
