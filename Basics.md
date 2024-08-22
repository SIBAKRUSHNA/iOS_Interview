   ##                                              iOS Developers Interview Basics Questions
### 1. What’s the difference between var and let? Which one would you choose for properties in a struct and why?
   -> var is used to declare variables whose values can change after they are initially set. You can reassign a new value to a var property.
-> let is used to declare constants whose values cannot change once they are assigned. Once a value is set for a let property, it cannot be 
             modified.
   ###                            Choosing Between var and let for Properties in a Struct
   -> In general, prefer let wherever possible to make your code safer and only use var when you need to allow changes to the property.
