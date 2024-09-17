## iOS Developers Interview SwiftUI Questions

 ### 1. What is SwiftUI?
  - SwiftUI is a modern declarative framework by Apple for building user interfaces across all Apple platforms.

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
