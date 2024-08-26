## iOS Developers Interview Higher-Order Functions Questions

- `Map`
     -  The map method create a new array by calling its callback method provide argument on every element of the input array.
       
```swift
let numbers = [1, 2, 3, 4]
let squaredNumbers = numbers.map { $0 * $0 }
```

- `CompactMap`
     - The compactMap  method remove nil value from the input array.
       
```swift
let strings = ["1", "2", "foo", "4"]
let numbers = strings.compactMap { Int($0) }

```

- `FlatMap`
     - The flatMap method similar as map but it is use when collection  inside that collection and convert to the single collection.

```swift
let arrays = [[1, 2], [3, 4]]
let flattened = arrays.flatMap { $0 }

```

- `Filter`
     - The filter method purpose is to filter the elements of the collection base on the condition and produce a new one containing only elements those elements that satisfy the condition.

```swift
let numbers = [1, 2, 3, 4]
let evenNumbers = numbers.filter { $0 % 2 == 0 }
```

- `Reduce`
     - The reduce method is to produce one value from the values of all elements in the collection.

```swift
let numbers = [1, 2, 3, 4]
let sum = numbers.reduce(0) { $0 + $1 }

```

- `ForEach`
     - The for each  method can be used in place of for-in loops in order to iterate through the elements of a collection.

```swift
let numbers = [1, 2, 3]
numbers.forEach { print($0) }
```

- `Contains`
     - The contains function is used in collection in order to check if there are elements that satisfy a certain condition and it return a boolean value.
 
```swift
let numbers = [1, 2, 3, 4]
let hasEven = numbers.contains { $0 % 2 == 0 }
```
