## iOS Developers Interview Initialization and DeInitialization Questions

### 1. How many types of Initialization?
- `Designated Initializer`
    - Designated initializers are the primary initializers for a class. A designated initializer fully initializes all properties introduced by that class and calls an appropriate superclass initializer to continue the initialization process up the superclass chain.
      
- `Convenience Initializer`
    - Convenience initializers are secondary, supporting initializers for a class. You can define a convenience initializer to call a designated initializer from the same class as the convenience initializer with some of the designated initializer’s parameters set to default values.
      
- `Required Initializer`
    - It's actually just a way of satisfying the compiler to assure it that if this class were to have any subclasses, they would inherit or implement this same initializer.
      
- `Failable Initializer`

### 2. What is Initializer Delegation?
  - Initializer can call other initializer to perform part of initialization, this process is known as initializer delegation.
