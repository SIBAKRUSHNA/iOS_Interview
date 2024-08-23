## iOS Developers Interview Subscripts Questions

### 1. What Subscripts in swift?
  - Subscripts are used to access information from a collection, sequence and a list in Classes, Structures and Enumerations 
    without using a method.

    ```swift
     struct MultiplicationTable {
    var multiplier: Int

    // Subscript to calculate the product for a given number
    subscript(index: Int) -> Int {
        return multiplier * index
       }
    }

    let table = MultiplicationTable(multiplier: 5)

    // Accessing the multiplication table using the subscript
    print(table[1])  // Output: 5
    print(table[2])  // Output: 10
    print(table[3])  // Output: 15
    print(table[10]) // Output: 50
     ```
