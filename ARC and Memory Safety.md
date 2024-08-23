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
    
### 8.

### 9.

### 10.
