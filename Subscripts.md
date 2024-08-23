## iOS Developers Interview Subscripts Questions

### 1. What Subscripts in swift?
  - Subscripts are used to access information from a collection, sequence and a list in Classes, Structures and Enumerations 
    without using a method.

    ```swift
     class WeekDays {
    private var days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]

    // Subscript definition
    subscript(index: Int) -> String? {
        get {
            if index >= 0 && index < days.count {
                return days[index]
            } else {
                return nil
            }
        }
        set {
            if let newValue = newValue, index >= 0 && index < days.count {
                days[index] = newValue
             }
         }
      }
    }
    
    let week = WeekDays()
    
    // Accessing elements using subscript
    print(week[0] ?? "Invalid Index") // Output: Sunday
    print(week[6] ?? "Invalid Index") // Output: Saturday

    // Modifying elements using subscript
    week[6] = "Funday"
    print(week[6] ?? "Invalid Index") // Output: Funday

    // Accessing an out-of-bound index
    print(week[7] ?? "Invalid Index") // Output: Invalid Index
  ```
