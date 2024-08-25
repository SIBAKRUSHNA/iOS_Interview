## iOS Developers Interview Auto Layout Questions

### 1. What is auto layout in swift
  - Auto Layout dynamically calculates the size and position of all the views in your view hierarchy, based on constraints placed on those views.
    
### 2. What is size class in swift?
  - Size Classes are groups of screen sizes that are applied to the width and height of the device screen.
    
### 3. How many types of size class in swift?
   `Compact` - Compact means narrow space.
   `Regular` - Regular means wider space.

   ![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*lOlo8WRtw-C37NSyZES5yQ.png)

### 4. What is content hugging and content compression resistance priority?
   - Hugging => Content does not want to grow.
   - Compression Resistance => Content does not want to shrink.
     
     ![](https://miro.medium.com/v2/resize:fit:2000/1*rIGewLhCwKyVkbXuI-ar8g.png)
     
### 5. What is constraints in autolayout in swift?
   - Constraints are rules that define how UI elements should be positioned and sized relative to each other and their container.
     
### 6. What is Autoresizing Masks?
   - Autoresizing masks define how a view resizes or moves in response to changes in its superview’s bounds.
     
### 7. What is leading and trailing in Swift?
  - `leading` - A view that appears on the leading edge of the title.
  - `trailing`- A view that appears on the trailing edge of the title.

### 8. What is left and right constraints?
  - Left and right constraints refer to constraints that specify the distances between the left and right edges of views or between a view and its superview.
    
### 9. What is the difference between anchor and constraints ?
  - `Anchors` - Anchors are properties of UIView (or its subclasses) that represent the edges and dimensions of a view.
  - `Constraints` - Constraints are the rules that define how views should be positioned and sized relative to each other or their superview.
    
### 10. What is the difference between leading constraint and left constraint?
  - `Leading Constraint` - A leading constraint defines the distance between the leading edge of a view and the leading edge of its container or another view.
  - `Left Constraint` - A left constraint specifies the distance between the left edge of a view and the left edge of its container or another view.

### 11. What is the difference between trailing constraint and right constraint?
  - `Trailing Constraint` - A trailing constraint defines the distance between the trailing edge of a view and the trailing edge of its container or another view.
  - `Right Constraint` - A right constraint specifies the distance between the right edge of a view and the right edge of its container or another view.
