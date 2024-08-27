## iOS Developers Interview Initialization and DeInitialization Questions

### 1. How many types of Initialization?
- `Designated Initializer`
- `Convenience Initializer`
- `Required Initializer`
    - It's actually just a way of satisfying the compiler to assure it that if this class were to have any subclasses, they would inherit or implement this same initializer.
      
- `Failable Initializer`

### 2. What is Initializer Delegation?
  - Initializer can call other initializer to perform part of initialization, this process is known as initializer delegation.
