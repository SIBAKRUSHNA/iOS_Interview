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
       
### 3. What is difference between enumerations and structures?
- `Enumerations`
     - Enums are used to define a type that can have one of a limited set of possible values. They are often used to represent a discrete set of 
       related values, such as options or states.
     - Commonly used for defining states, categories, or options, such as days of the week, direction (north, south, east, west), or error codes.
       
- `Structures`
     - Structs are used to define complex data types that group related data together. They can store multiple values and encapsulate related 
       functionality.
     - Commonly used for modeling real-world entities with multiple properties, such as coordinates, shapes, or user data.

### 4. What is associated values enum swift?
  -  Associated values allow you to store additional data alongside each case in an enumeration

### 5. What caseiterable enum swift?
  - CaseIterable protocol that automatically generates an array property of all cases in an enum.
