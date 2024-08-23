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
![](data:image/png;base64,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)

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
