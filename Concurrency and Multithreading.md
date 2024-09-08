## iOS Developers Interview Concurrency and Multithreading Questions

### 1. What is multithreading?
  - Multithreading in Swift allows you to perform multiple tasks simultaneously, which can help improve the performance and 
   responsiveness of your application.

### 2. What is concurrency?
  - Concurrency in Swift refers to the ability of a program to execute multiple tasks or operations simultaneously.

### 3. What is GCD?
  - Grand Central Dispatch or GCD is a low-level API for managing concurrent operations.
    
### 4. What is NSOperation?
  - NSOperation is a class in Swift used for managing and executing operations concurrently.

### 5. What is synchronous and asynchronous? 
  - `Synchronous`
        - Synchronous execution means that tasks are performed sequentially. Each task must complete before the next one starts.
  - `Asynchronous`
        - Asynchronous execution allows tasks to run concurrently, meaning that other tasks can continue running without waiting for the current task to complete.
    
### 6. What is async await?
  - Async await is a mechanism used to create and execute asynchronous functions.
    ```swift
    func processData() async {
    let data = await fetchData() // Wait for fetchData to complete
    print("Data processed: \(data)")
    }
    Task {
     await processData() // Call the asynchronous function
    }
    ```
### 7. When to use dispatch barrier?
  -  It ensures that the task you submit with the barrier flag will only execute after all previously submitted tasks on that queue have finished.
```swift
let queue = DispatchQueue(label: "com.example.queue", attributes: .concurrent)
var sharedResource = [String]()

func addToSharedResource(item: String) {
    queue.async(flags: .barrier) {
        sharedResource.append(item)
    }
}

func readFromSharedResource(completion: @escaping ([String]) -> Void) {
    queue.async {
        completion(sharedResource)
    }
}

```
### 8. What is quality of services?
- The quality of service, or the execution priority, to apply to tasks. It allows you to manage the execution priority of tasks in your app.
  
 - `userInteractive`
    - Priority: Highest
    - Purpose: For tasks that must be done immediately to keep the app responsive.
    - Example: Handling a button tap or updating the screen.
- `userInitiated`
    - Priority: High
    - Purpose: For tasks that the user expects to be completed quickly but aren't as urgent as UI updates.
    - Example: Loading content after the user requests it.
- `unspecified`
    - Priority: Not set
    - Purpose: The system decides the priority. Use when you don't have specific requirements.
    - Example: Legacy code or when no priority is needed.
- `default`
    - Priority: Not set
    - Purpose: For general tasks that don't need to be completed immediately but should still be done soon.
    - Example: Standard app operations that aren't time-sensitive.
- `utility`
    - Priority: Medium
    - Purpose: For tasks that take longer and don't need to be completed right away.
    - Example: Downloading files or processing large amounts of data.
- `background`
    - Priority: Low
    - Purpose: For tasks that the user isn't directly aware of and can be done when the system has resources available.
    - Example: Syncing data or performing backup
  
### 9. What is a Deadlock?
  - Deadlock occurs when two or more threads are blocked  unspecified period of time., waiting for each other to release a resource.
    
### 10. How to avoid deadlock situation?
  - Use higher-level synchronization mechanisms provided by GCD (Grand Central Dispatch) and NSOperationQueue.
  - Avoid Synchronous Calls on the Main Queue.
  - Avoid Nested Synchronous Calls Across Different Queues

### 11. What is a Race Condition?
  - A race condition in iOS app development happens when two or more tasks try to access 
    shared resources at the same time, leading to unpredictable behaviour.

### 12 What is thread safe in swift?
  -  Multiple threads can access shared resources (like variables, objects, or data structures) without causing data corruption or inconsistencies.
    
### 13. What is the difference between DispatchQueue sync vs sync barrier in concurrent queue?
   - 

### 14. What is the difference between DispatchQueue async vs async barrier in concurrent queue?
   - 
### 15. What is semaphore in swift?
   - Semaphore is a synchronization mechanism used to manage access to a shared resource by multiple threads.

### 16. How to cancel a thread in swift?
   - Using dispatch queue cancel method.
     
### 17. What is dispatchGroup?
   - A group of tasks that you monitor as a single unit.

### 18. What is atomic and non-atomic in swift?
  - `Atomic` - Atomic means only one thread accesses the variable (static type). Atomic is 
               thread-safe, but it is slow.
  - `Nonatomic` - Nonatomic means multiple threads access the variable (dynamic type). 
                  Nonatomic is thread-unsafe, but it is fast.
    
### 19. What is actor in swift?
  - In Swift, an actor is a reference type that was introduced in Swift 5.5 as part of its advanced concurrency model.

``` swift
actor Counter {
    private var count = 0
    
    func increment() {
        count += 1
    }
    
    func getCount() -> Int {
        return count
    }
}
let counter = Counter()

Task {
    // Increment the count
    await counter.increment()
    await counter.increment()

    // Get the current count
    let currentCount = await counter.getCount()
    print("Current count: \(currentCount)") // Output: Current count: 2
}
```
### 20. What difference between GCD and operation queue Swift?
  - Use GCD when you need a lightweight and efficient way to perform simple asynchronous tasks.
  - Use Operation Queue when you require more control over task dependencies, cancellation, or need to encapsulate tasks as Operation objects.

### 21. What is the difference between async/await and Actor?
- `Async/await:`
    - Focuses on managing asynchronous operations by making them easier to read and write.
    - Does not inherently prevent race conditions or handle thread safety.
    - Provides a way to "pause" and "resume" tasks in a non-blocking way.
- `Actors:`
    - Focuses on ensuring thread safety by serializing access to its mutable state.
    - Helps prevent race conditions without requiring explicit locking.
    - Can have async methods, so they often work in combination with async/await.
