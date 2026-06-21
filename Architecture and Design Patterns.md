## iOS Developers Interview Architecture and Design Patterns Questions

# 1. What is delegate? 
  - Delegates are a design pattern that allows one object to send messages to another object when a specific event happens.

A **Delegate** is a design pattern used to pass data or events from one object to another.

It allows one object to communicate with another object without creating a strong dependency between them.

---

## 🎯 Why Use Delegate?

* Pass data between screens
* Handle user actions
* Reduce tight coupling
* Follow Single Responsibility Principle
* Improve code reusability

---

## 🔄 Delegate Flow

```text
Sender Object
      │
      ▼
Delegate Protocol
      │
      ▼
Receiver Object
```

---

## 📝 Step 1: Create a Protocol

```swift
protocol UserDelegate: AnyObject {
    func didSelectUser(name: String)
}
```

---

## 📝 Step 2: Create Delegate Property

```swift
class SecondViewController: UIViewController {

    weak var delegate: UserDelegate?

    func sendData() {
        delegate?.didSelectUser(name: "Siba")
    }
}
```

---

## 📝 Step 3: Conform to Protocol

```swift
class FirstViewController: UIViewController {

}

extension FirstViewController: UserDelegate {

    func didSelectUser(name: String) {
        print(name)
    }
}
```

---

## 📝 Step 4: Assign Delegate

```swift
let secondVC = SecondViewController()
secondVC.delegate = self
```

---

## 🚀 Real-Life Examples

### UITableViewDelegate

```swift
tableView.delegate = self
```

### UICollectionViewDelegate

```swift
collectionView.delegate = self
```

### UITextFieldDelegate

```swift
textField.delegate = self
```

---

## ⚡ Advantages

* Loose Coupling
* Better Code Organization
* Reusable Components
* Easy Event Handling
* Widely Used in UIKit

---

## 🎤 Interview Questions

### 1. What is Delegate Pattern?

A communication pattern where one object delegates responsibilities to another object.

### 2. Why is delegate usually weak?

To avoid a retain cycle and memory leak.

### 3. What does AnyObject mean in a protocol?

It restricts the protocol to class types, allowing weak references.

### 4. What is the difference between Delegate and Notification?

* Delegate → One-to-One communication
* Notification → One-to-Many communication

### 5. Where is Delegate commonly used?

* UITableView
* UICollectionView
* UITextField
* CLLocationManager

---

## 📌 Quick Summary

```text
Delegate = One-to-One Communication

Protocol
   ↓
Delegate Property
   ↓
Assign Delegate
   ↓
Call Delegate Method
   ↓
Receive Data/Event
```

💡 Delegate is one of the most commonly asked iOS interview topics and is heavily used throughout UIKit.

<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 10_55_37 PM" src="https://github.com/user-attachments/assets/f1b8a95b-7226-43d6-9ff2-de813ae5245b" />

    
# 2. What is singleton design pattern?
  - Singleton is a design pattern that ensures a class can have only one object.

## 🎯 Why Use Singleton?

* Shared Resources
* Global Access
* Memory Efficient
* Centralized Data Management
* Avoid Multiple Instances

---

## 🏗️ Singleton Structure

```text id="wjrm4q"
Class
  │
  ├── private init()
  │
  └── static let shared
           │
           ▼
     Single Instance
```

---

## 📝 Example

```swift id="vj5lm5"
final class NetworkManager {

    static let shared = NetworkManager()

    private init() { }

    func fetchData() {
        print("Fetching Data...")
    }
}
```

### Usage

```swift id="3e4p6g"
NetworkManager.shared.fetchData()
```

---

## 🔄 How It Works

```text id="sxyi7r"
App Launch
     │
     ▼
NetworkManager.shared
     │
     ▼
Single Instance Created
     │
     ▼
Used Everywhere
```

---

## 🚀 Real-Life Examples in iOS

### UserDefaults

```swift id="otc8c4"
UserDefaults.standard
```

### FileManager

```swift id="tekhvo"
FileManager.default
```

### URLCache

```swift id="vz6m7w"
URLCache.shared
```

### NotificationCenter

```swift id="3u3n2v"
NotificationCenter.default
```

---

## ✅ Advantages

* Global Access Point
* Single Source of Truth
* Saves Memory
* Easy to Access
* Shared State Management

---

## ❌ Disadvantages

* Harder Unit Testing
* Global State Issues
* Tight Coupling
* Hidden Dependencies
* Can Become a God Object

---

## 🎤 Interview Questions

### 1. What is Singleton Pattern?

A design pattern that allows only one instance of a class throughout the application.

### 2. How do you create a Singleton in Swift?

Using a static shared instance and a private initializer.

### 3. Why is init() private?

To prevent creating multiple instances.

### 4. Name some Singleton classes in iOS.

* UserDefaults
* FileManager
* NotificationCenter
* URLCache

### 5. What are the drawbacks of Singleton?

* Difficult to test
* Global state management issues
* Tight coupling

### 6. When should you use Singleton?

When a single shared instance is required across the entire application.

---

## ⚡ Quick Summary

```text id="azv1ke"
Singleton

static let shared
        │
private init()
        │
One Instance
        │
Global Access
```

### Example

```swift id="a5yn4m"
class APIManager {

    static let shared = APIManager()

    private init() { }
}
```

💡 **Remember:** Singleton = **One Instance + Global Access Point**

<img width="1024" height="1536" alt="ChatGPT Image Jun 22, 2026, 12_07_07 AM" src="https://github.com/user-attachments/assets/a4ec638e-2c67-4041-8601-7bbf99841594" />

    
# 3. What is disadvise and advertise in singleton design pattern?
- `Advantages`
     - Improved memory usage: Singleton design pattern can reduce the memory usage of an application.
     - Simplified access and control: It can simplify the access and control of a shared resource.
     
- `Disadvantages`
     - Increased complexity and risk: It can introduce tight coupling and hidden dependencies in code.
     - Violates Single Responsibility Principle: Singleton design pattern can violate the Single Responsibility Principle.
           - Controlling the Instance
           - Performing Business Logic

# 4. What is MVC Architecture in iOS?
 - `Model` - Models are representations of your your app’s data.
 - `View` - Views are objects that users of your app can see and interact with. View objects should be reusable and flexible.
 - `Controller` - Controllers mediate between the View and the Model.

## 🏗️ MVC Components

## 1️⃣ Model

Responsible for:

* Data
* Business Logic
* API Response Models
* Database Objects

### Example

```swift id="g7b6kc"
struct User {
    let id: Int
    let name: String
}
```

---

## 2️⃣ View

Responsible for:

* Displaying UI
* User Interaction
* Buttons
* Labels
* TextFields

### Example

```swift id="8yw3c3"
@IBOutlet weak var nameLabel: UILabel!
```

---

## 3️⃣ Controller

Responsible for:

* Managing Views
* Receiving User Actions
* Updating UI
* Communicating with Model

### Example

```swift id="cw0vdy"
class UserViewController: UIViewController {

    @IBOutlet weak var nameLabel: UILabel!

    override func viewDidLoad() {
        super.viewDidLoad()

        let user = User(id: 1, name: "Siba")
        nameLabel.text = user.name
    }
}
```

---

## 🔄 MVC Flow

```text id="3af2wc"
User Action
      │
      ▼
     View
      │
      ▼
 Controller
      │
      ▼
    Model
      │
      ▼
 Controller
      │
      ▼
     View
```

---

## 📂 MVC Structure

```text id="8jpx9r"
Project
│
├── Models
│   └── User.swift
│
├── Views
│   └── UserView.xib
│
└── Controllers
    └── UserViewController.swift
```

---

## 🚀 Advantages

* Easy to Learn
* Apple's Default Pattern
* Simple for Small Projects
* Quick Development
* Good UIKit Support

---

## ❌ Disadvantages

* Massive View Controller Problem
* Hard to Test
* Tight Coupling
* Difficult to Scale
* Business Logic Often Ends Up in ViewController

---

## ⚠️ Massive View Controller

A common issue in MVC:

```swift id="r4j8v7"
class UserViewController: UIViewController {

    func fetchUsers() {}
    func saveUsers() {}
    func validateUser() {}
    func callAPI() {}
    func updateUI() {}
    func handleNavigation() {}
}
```

The ViewController becomes too large and manages everything.

This is known as:

### 👉 Massive View Controller

---

## 🎤 Interview Questions

### 1. What is MVC?

A design pattern that separates an application into Model, View, and Controller.

### 2. What does Model contain?

Data and business logic.

### 3. What does View contain?

UI components such as labels, buttons, and text fields.

### 4. What is the role of Controller?

Acts as a mediator between Model and View.

### 5. What is the biggest drawback of MVC?

Massive View Controller.

### 6. Why do developers move to MVVM?

To reduce ViewController responsibilities and improve testability.

---

## ⚡ Quick Summary

```text id="yfdcqs"
Model
  ↓
Controller
  ↓
View

MVC = Model + View + Controller
```

### Responsibilities

```text id="tt0n7l"
Model      → Data
View       → UI
Controller → Logic & Coordination
```

💡 **Remember:** MVC is simple and widely used, but in large projects it often leads to **Massive View Controllers**, which is why architectures like MVVM and Clean Architecture are preferred.

<img width="1024" height="1536" alt="ChatGPT Image Jun 22, 2026, 12_23_35 AM" src="https://github.com/user-attachments/assets/9915bca0-1465-4f62-91e5-f8dfa064e0f5" />


# 5. What is MVVM Architecture in iOS?
 - `Model` - Models are classes or structures that hold data.
 - `View` - Views refer to the UI elements which show data to the users and take data from the users.
 - `View-Model` - View-Model is the mediatory layer between model and view.

## 🏗️ MVVM Components

## 1️⃣ Model

Responsible for:

* Data Models
* Business Objects
* API Response Models

### Example

```swift
struct User {
    let id: Int
    let name: String
}
```

---

## 2️⃣ View

Responsible for:

* Displaying UI
* Handling User Interaction
* Showing Data from ViewModel

### Example

```swift
class UserViewController: UIViewController {
    
    @IBOutlet weak var nameLabel: UILabel!
}
```

---

## 3️⃣ ViewModel

Responsible for:

* Business Logic
* Data Transformation
* API Calls
* Providing Data to View

### Example

```swift
class UserViewModel {

    var userName: String = ""

    func fetchUser() {
        let user = User(id: 1, name: "Siba")
        userName = user.name
    }
}
```

---

## 🔄 MVVM Flow

```text
User Action
      │
      ▼
     View
      │
      ▼
  ViewModel
      │
      ▼
    Model
      │
      ▼
  ViewModel
      │
      ▼
     View
```

---

## 📂 Folder Structure

```text
Project
│
├── Models
│   └── User.swift
│
├── Views
│   └── UserViewController.swift
│
├── ViewModels
│   └── UserViewModel.swift
│
└── Services
    └── APIService.swift
```

---

## 📝 Example

### Model

```swift
struct User {
    let name: String
}
```

### ViewModel

```swift
class UserViewModel {

    private let user = User(name: "Siba")

    var userName: String {
        return user.name
    }
}
```

### ViewController

```swift
class UserViewController: UIViewController {

    @IBOutlet weak var nameLabel: UILabel!

    let viewModel = UserViewModel()

    override func viewDidLoad() {
        super.viewDidLoad()

        nameLabel.text = viewModel.userName
    }
}
```

---

## MVC vs MVVM

| MVC                          | MVVM                        |
| ---------------------------- | --------------------------- |
| Business Logic in Controller | Business Logic in ViewModel |
| Massive View Controller      | Smaller View Controller     |
| Harder to Test               | Easier to Test              |
| Tight Coupling               | Better Separation           |
| Less Scalable                | More Scalable               |

---

## 🚀 Advantages

* Better Separation of Concerns
* Easy Unit Testing
* Reusable ViewModels
* Cleaner Code
* Scalable Architecture
* Reduced ViewController Size

---

## ❌ Disadvantages

* More Files
* Slightly Higher Complexity
* Learning Curve for Beginners

---

## 🎤 Interview Questions

### 1. What is MVVM?

MVVM is an architecture pattern that separates UI, business logic, and data using Model, View, and ViewModel.

### 2. What is the role of ViewModel?

ViewModel contains presentation and business logic and prepares data for the View.

### 3. Does ViewModel know about View?

No. ViewModel should not directly reference the View.

### 4. What problem does MVVM solve?

It reduces the Massive View Controller problem found in MVC.

### 5. Why is MVVM more testable?

Because business logic is moved from ViewController to ViewModel.

### 6. Can MVVM be used with Combine?

Yes. MVVM works very well with:

* Combine
* RxSwift
* Async/Await

---

## ⚡ Quick Summary

```text
Model
  ↑
ViewModel
  ↑
View
```

### Responsibilities

```text
Model      → Data

ViewModel  → Business Logic
             Data Transformation

View       → UI
```

### Flow

```text
View
  ↓
ViewModel
  ↓
Model
  ↓
ViewModel
  ↓
View
```

💡 **Remember:** MVVM moves business logic from the ViewController into a ViewModel, making the app easier to maintain, test, and scale.

<img width="1024" height="1536" alt="ChatGPT Image Jun 22, 2026, 12_34_18 AM" src="https://github.com/user-attachments/assets/4f30d9d1-44e0-4edf-9536-e29352a04afe" />

   
# 6. What is the disadvantages of MVVM?
  -  `ViewModel Bloat`
     - `Issue`: The ViewModel can become bloated if too much business logic or UI-related code is added to it.
     - `Impact`: This results in hard-to-maintain code, as it can become challenging to separate concerns. Developers might inadvertently add View logic in the ViewModel, which goes against MVVM principles.

  - `Difficult Binding with UIKit`
     - `Issue`: UIKit doesn’t have built-in support for data binding, which makes implementing MVVM more challenging.
     - `Impact`: Developers often need to rely on libraries like RxSwift or Combine to implement reactive bindings, adding extra dependencies and complexity.

# 7.  🏗️ Clean Architecture in iOS (Swift)

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

## 🏛️ Architecture Layers

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

## 🔄 Data Flow

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

## 📂 Folder Structure

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

## 🔗 Dependency Rule

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

## 🎤 Interview Questions

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

## ⚡ Quick Summary

```text
Presentation → UI Layer

Domain → Business Logic

Data → API / Database

Flow:
View → ViewModel → UseCase → Repository → API/DB
```

💡 Clean Architecture helps build scalable, maintainable, and testable iOS applications.

<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 10_39_14 PM" src="https://github.com/user-attachments/assets/8bb3f216-fe30-4ab0-8184-eff89c3ddb3d" />


# 8. What is VIPER Architecture in iOS?

**VIPER** is an iOS architecture pattern that divides an application into five separate layers:

* **V** → View
* **I** → Interactor
* **P** → Presenter
* **E** → Entity
* **R** → Router

VIPER provides a highly modular, scalable, and testable architecture.

---

## 🏗️ VIPER Components

## 1️⃣ View

### Responsibilities

* Display UI
* Handle User Actions
* Forward Events to Presenter

```swift id="8d4z2m"
protocol UserViewProtocol: AnyObject {
    func showUsers()
}
```

---

## 2️⃣ Interactor

### Responsibilities

* Business Logic
* API Calls
* Database Operations
* Data Processing

```swift id="63hj5f"
protocol UserInteractorProtocol {
    func fetchUsers()
}
```

---

## 3️⃣ Presenter

### Responsibilities

* Connect View and Interactor
* Handle Presentation Logic
* Update View

```swift id="x2myxk"
class UserPresenter {

    var view: UserViewProtocol?
    var interactor: UserInteractorProtocol?

    func loadUsers() {
        interactor?.fetchUsers()
    }
}
```

---

## 4️⃣ Entity

### Responsibilities

* Data Models
* Business Objects

```swift id="84jvyl"
struct User {
    let id: Int
    let name: String
}
```

---

## 5️⃣ Router

### Responsibilities

* Navigation
* Screen Routing
* Module Creation

```swift id="5jjc1v"
class UserRouter {

    static func createModule() -> UIViewController {
        return UserViewController()
    }
}
```

---

## 🔄 VIPER Flow

```text id="m2n9ye"
User Action
      │
      ▼
     View
      │
      ▼
   Presenter
      │
      ▼
  Interactor
      │
      ▼
    Entity
      │
      ▼
  Interactor
      │
      ▼
   Presenter
      │
      ▼
     View
```

---

## 🧭 Navigation Flow

```text id="q4j3eo"
View
  │
  ▼
Presenter
  │
  ▼
Router
  │
  ▼
Next Screen
```

---

## 📂 Folder Structure

```text id="8ff7gt"
UserModule
│
├── View
│   └── UserViewController.swift
│
├── Presenter
│   └── UserPresenter.swift
│
├── Interactor
│   └── UserInteractor.swift
│
├── Entity
│   └── User.swift
│
└── Router
    └── UserRouter.swift
```

---

## MVC vs MVVM vs VIPER

| MVC              | MVVM              | VIPER                 |
| ---------------- | ----------------- | --------------------- |
| 3 Layers         | 3 Layers          | 5 Layers              |
| Massive VC       | Better Separation | Maximum Separation    |
| Moderate Testing | Easy Testing      | Excellent Testing     |
| Easy Setup       | Medium Complexity | High Complexity       |
| Small Apps       | Medium/Large Apps | Large Enterprise Apps |

---

## 🚀 Advantages

* Highly Modular
* Excellent Testability
* Clear Separation of Concerns
* Scalable for Large Projects
* Easier Team Collaboration
* Smaller Classes

---

## ❌ Disadvantages

* Too Many Files
* Boilerplate Code
* Higher Learning Curve
* Overkill for Small Projects
* Setup Takes More Time

---

## 🎤 Interview Questions

### 1. What does VIPER stand for?

* View
* Interactor
* Presenter
* Entity
* Router

### 2. Which layer contains business logic?

**Interactor**

### 3. Which layer handles navigation?

**Router**

### 4. What is the role of Presenter?

Acts as a mediator between View and Interactor.

### 5. Why is VIPER highly testable?

Because each component has a single responsibility and communicates through protocols.

### 6. When should you use VIPER?

For large, complex, enterprise-level applications.

---

## ⚡ Quick Summary

```text id="6qk1zk"
View
  ↓
Presenter
  ↓
Interactor
  ↓
Entity

Navigation
Presenter
  ↓
Router
```

### Responsibilities

```text id="tuzm8m"
View       → UI

Interactor → Business Logic

Presenter  → Presentation Logic

Entity     → Data Model

Router     → Navigation
```

💡 **Remember:** VIPER provides the best separation of concerns among iOS architectures, but it comes with more files and complexity. It is commonly used in large-scale enterprise applications.

<img width="1024" height="1536" alt="ChatGPT Image Jun 22, 2026, 12_48_04 AM" src="https://github.com/user-attachments/assets/9882bb6b-ad30-4f6d-9ce1-7f7b097b044f" />


# 9.

# 10.

# 11.
