## iOS Developers Interview Architecture and Design Patterns Questions

### 1. What is delegate? 
  - Delegates are a design pattern that allows one object to send messages to another object when a specific event happens.
    
### 2. What is singleton design pattern?
  - Singleton is a design pattern that ensures a class can have only one object.
    
### 3. What is disadvise and advertise in singleton design pattern?
- `Advantages`
     - Improved memory usage: Singleton design pattern can reduce the memory usage of an application.
     - Simplified access and control: It can simplify the access and control of a shared resource.
     
- `Disadvantages`
     - Increased complexity and risk: It can introduce tight coupling and hidden dependencies in code.
     - Violates Single Responsibility Principle: Singleton design pattern can violate the Single Responsibility Principle.
           - Controlling the Instance
           - Performing Business Logic

### 4. What is MVC Architecture in iOS?
 - `Model` - Models are representations of your your app’s data.
 - `View` - Views are objects that users of your app can see and interact with. View objects should be reusable and flexible.
 - `Controller` - Controllers mediate between the View and the Model.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*MQxIn8fG3UrLxqy4Q_dR_w.png)
   
### 5. What is MVVM Architecture in iOS?
 - `Model` - Models are classes or structures that hold data.
 - `View` - Views refer to the UI elements which show data to the users and take data from the users.
 - `View-Model` - View-Model is the mediatory layer between model and view.

 ![](https://i.sstatic.net/AIPW4.png)
   
### 6. What is the disadvantages of MVVM?
  -  `ViewModel Bloat`
     - `Issue`: The ViewModel can become bloated if too much business logic or UI-related code is added to it.
     - `Impact`: This results in hard-to-maintain code, as it can become challenging to separate concerns. Developers might inadvertently add View logic in the ViewModel, which goes against MVVM principles.

  - `Difficult Binding with UIKit`
     - `Issue`: UIKit doesn’t have built-in support for data binding, which makes implementing MVVM more challenging.
     - `Impact`: Developers often need to rely on libraries like RxSwift or Combine to implement reactive bindings, adding extra dependencies and complexity.

### 7.

### 8.

### 9.

### 10.

### 11.
