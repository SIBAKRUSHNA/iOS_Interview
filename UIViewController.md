## iOS Developers Interview UIViewController Questions

### 1. What is the UIViewController parent class ?
  - UIResponder

### 2. What is the @IBOutlet?
  - The type qualifier IBOutlet is a tag applied to an property declaration so that the Interface Builder application can recognize the property as an outlet and synchronize the display and connection of it with  Xcode.

### 3. Differences between `layoutIfNeeded()` and `setNeedsLayout()`:
  - `setNeedsLayout()`: Marks the view as needing an update, but doesn't immediately update the layout. UIKit will perform the layout update at the next appropriate opportunity.
  - `layoutIfNeeded()`: Forces the layout update right away.

```swift
myView.setNeedsLayout()  // Marks the view for layout update
myView.layoutIfNeeded()  // Immediately applies the layout updates
```
