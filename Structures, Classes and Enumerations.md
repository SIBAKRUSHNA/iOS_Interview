## iOS Developers Interview Structures, Classes and Enumerations Questions

### 1. What is the difference between class and structure?
- `Class`
   - Classes are reference types.
   - Classes support inheritance.
   - Classes can have deinitializers (deinit) that are called when an instance of the class is deallocated.
   - When a class instance is assigned to a constant, its properties can still be changed if they are declared as var within the class.

- `Structures`
   - Structures are value types.
   - Structures do not support inheritance.
   - Structures do not have deinitializers since they are value types and are automatically deallocated when they go out of scope.
   - When a structure instance is assigned to a constant, all of its properties become immutable, even if they are declared as var within the 
     structure.
     
### 2. What is the difference between value types and reference types?

- `Reference Types`
     - Value types are types where each instance keeps a unique copy of its data.
     - Classes (class): Classes in Swift are reference types.
- `Value Types`
     -  Reference types are types where instances share a single copy of the data.
     -  Structures (struct): Structures in Swift are value types.
