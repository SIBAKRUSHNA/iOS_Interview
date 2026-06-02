## iOS Developers Interview SwiftUI Questions

 ### 1. What is SwiftUI?
  - SwiftUI is a modern declarative framework by Apple for building user interfaces across all Apple platforms.

<img width="1024" height="1536" alt="ChatGPT Image Jun 2, 2026, 09_31_33 PM" src="https://github.com/user-attachments/assets/6480fe19-51b9-4b7e-894d-939899731dca" />


 ### 2. What is some in swiftUI?
  - We learned that the “some” keyword signifies an opaque type
    
 ### 3. What is VStack in swiftUI?
   - A VStack works exactly like an HStack, but in the vertical direction.

 ### 4. What is HStack in swiftUI?
   - A view that arranges its subviews in a horizontal line.

 ### 5. What is ZStack in swiftUI?
   - The ZStack view is a layout container where elements, or subviews, are arranged as overlaying one another

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Q5PisUZG2BoJYvfHExMiow.png)

### 6. What is the difference between uikit and swiftUI?
  -  SwitUI is a declarative framework but UIKit is an imperative framework

### 7. what is @envarevent in swiftUI?
  - The @Environment property wrapper in SwiftUI allows you to read values from a view’s environment. 

### 8. What is @State in swiftUI ?
  - In SwiftUI, @State is a property wrapper that manages local state within a view.

### 9. What is @Binding in swiftUI ?
  - In Swift, @Binding is a property wrapper used in SwiftUI to create a two-way connection between a view and its 
    underlying data.

### 10. What is @Published in swiftUI ?
  - @Published is a property wrapper in SwiftUI that lets you mark a property of a class as observable

### 11. What is @ObservedObject in swiftUI ?
  -  In SwiftUI, @ObservedObject is a property wrapper used to create a reference to an observable object, which is a class 
     conforming to the ObservableObject protocol. This allows the view to automatically update whenever the observable 
     object changes.

### 12. What is @EnvironmentObject in swiftUI ?
  - In SwiftUI, @EnvironmentObject is a property wrapper used to share data across the entire view hierarchy without having 
    to pass the data explicitly from parent to child views. It allows views to access and observe shared data from the 
    environment.

### 13. What is @StateObject in swiftUI ?
  - In SwiftUI, @StateObject is a property wrapper used to create and manage the lifecycle of an observable object. It is 
    used to initialize and own an instance of an ObservableObject in a view, ensuring that the object is created only once 
    and persists for the lifetime of the view.

### 14. @StateObject vs. @ObservedObject: The differences explained
  - `@StateObject`:
       - Suitable for views that create and maintain the state of an object, like data models or view models.
  - `@ObservedObject`:
       - Best used when a view is given an observable object by a parent and should observe it without owning or reinitializing it.

### 14. What is GeometryReader?
  - A container view that defines its content as a function of its own size and coordinate space.
    
### 15. What is grid in swiftUI?
  - A grid in SwiftUI is a container view that organizes other views in a two-dimensional layout

### 16. How to use uikit components in swiftUI?
  - In SwiftUI, you can integrate UIKit components using the `UIViewRepresentable` and `UIViewControllerRepresentable` protocols.
    
### 16. What publicer and subscriber in swiftUI?
  - In other words: Publishers are the source of data and subscribers are the consumers of that data.

### 17. What is combine framework in swiftUI?
  - The Combine framework provides a declarative Swift API for processing values over time.

### 18. What is @ViewBuilder in SwiftUI?
  - @ViewBuilder is a SwiftUI result builder that combines multiple views into a single view hierarchy and enables declarative UI construction.
    - @ViewBuilder is a result builder provided by SwiftUI.
    - It allows multiple views to be declared inside a closure, function, or computed property.
    - SwiftUI automatically combines these views into a single view hierarchy.
    - It supports conditional statements such as if, else, and switch.
    - It is used internally by the body property of SwiftUI views.
```swift
  @ViewBuilder
   func contentView(isLoggedIn: Bool) -> some View {
     if isLoggedIn {
        Text("Welcome")
      } else {
        Text("Login")
     }
  }
```
### 19. What is @Observable in SwiftUI?
- @Observable is a Swift macro introduced in iOS 17 that automatically tracks property changes and updates SwiftUI views.
   ## Key Points:
  - Part of the Observation framework.
  - Replaces ObservableObject and @Published in many cases.
  - Reduces boilerplate code.
  - SwiftUI automatically refreshes when data changes.

  ## Example:
```swift
import Observation

@Observable
class UserViewModel {
    var name = "John"
}
```
