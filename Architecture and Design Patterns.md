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

### 7. # 🏗️ Clean Architecture in iOS (Swift)

## 📖 What is Clean Architecture?

Clean Architecture is a software design pattern that separates an application into independent layers. It improves maintainability, scalability, and testability by keeping business logic separate from UI and data sources.

---

## 🎯 Goals

* ✅ Separation of Concerns
* ✅ Easy Unit Testing
* ✅ Scalability
* ✅ Maintainability
* ✅ Reusable Business Logic

---

# 🏛️ Architecture Layers

```text
┌─────────────────────┐
│    Presentation     │
│  View / ViewModel   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│       Domain        │
│ UseCases / Entities │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│        Data         │
│ Repository / API DB │
└─────────────────────┘
```

---

## 1️⃣ Presentation Layer

### Responsibilities

* Display UI
* Handle User Actions
* Call Use Cases
* Update Views

### Components

* UIViewController
* SwiftUI View
* ViewModel

---

## 2️⃣ Domain Layer

### Responsibilities

* Business Logic
* Application Rules
* Use Cases
* Entity Models

### Components

* Entities
* Use Cases
* Repository Protocols

### Example Entity

```swift
struct User {
    let id: Int
    let name: String
}
```

---

## 3️⃣ Data Layer

### Responsibilities

* API Calls
* Database Operations
* Repository Implementations
* Data Mapping

### Components

* API Service
* Local Database
* DTO Models
* Repository Implementation

---

# 🔄 Data Flow

```text
User Action
      ↓
ViewController
      ↓
ViewModel
      ↓
UseCase
      ↓
Repository
      ↓
API / Database
      ↓
Response
      ↓
ViewModel
      ↓
UI Update
```

---

# 📂 Folder Structure

```text
Project
│
├── Presentation
│   ├── Views
│   ├── ViewModels
│   └── Coordinators
│
├── Domain
│   ├── Entities
│   ├── UseCases
│   └── Repositories
│
├── Data
│   ├── Network
│   ├── Repository
│   ├── DTOs
│   └── Database
│
└── Core
    ├── DependencyInjection
    ├── Extensions
    └── Utilities
```

---

# 🔗 Dependency Rule

```text
Presentation
      ↓
   Domain
      ↓
    Data
```

### Important Rules

✅ Data Layer depends on Domain Protocols

❌ Domain Layer should NOT depend on:

* UIKit
* SwiftUI
* Networking
* Database

---

# 🚀 Benefits

* Easy Unit Testing
* Better Code Organization
* Loose Coupling
* Reusable Business Logic
* Faster Development
* Easier Maintenance
* Scalable for Large Projects

---

# 🎤 Interview Questions

### 1. What is Clean Architecture?

A layered architecture pattern that separates UI, business logic, and data layers.

### 2. What are the main layers?

* Presentation
* Domain
* Data

### 3. Which layer contains business logic?

Domain Layer.

### 4. What is a Use Case?

A class that encapsulates a specific business operation.

### 5. Why use Repository Pattern?

To abstract data sources and improve testability.

### 6. Can Domain depend on UIKit?

No. Domain must remain framework-independent.

### 7. What is Dependency Injection?

Providing dependencies from outside instead of creating them inside a class.

### 8. Why is Clean Architecture testable?

Because layers are loosely coupled and dependencies can be mocked.

---

# ⚡ Quick Summary

```text
Presentation → UI Layer

Domain → Business Logic

Data → API / Database

Flow:
View → ViewModel → UseCase → Repository → API/DB
```

💡 Clean Architecture helps build scalable, maintainable, and testable iOS applications.

<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 10_39_14 PM" src="https://github.com/user-attachments/assets/8bb3f216-fe30-4ab0-8184-eff89c3ddb3d" />


### 8.

### 9.

### 10.

### 11.
