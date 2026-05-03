## iOS Developers Interview Concurrency and Multithreading Questions

### 1. What is multithreading?
  - Multithreading in Swift allows you to perform multiple tasks simultaneously, which can help improve the performance and 
   responsiveness of your application.

### 2. What is concurrency?
  - Concurrency in Swift refers to the ability of a program to execute multiple tasks or operations simultaneously.
  - Concurrency is used to:
    - Keep UI smooth (main thread free)
    - Run heavy tasks in background
  - Common tools:
    - GCD (Grand Central Dispatch)
    - OperationQueue
    - async/await (modern Swift)

### 3. What is GCD?
  - Grand Central Dispatch or GCD is a low-level API for managing concurrent operations.
  - 🔹 Why GCD is used?
     - To perform background tasks (API calls, file I/O, heavy computation)
     - To keep the UI responsive
     - To avoid manually creating and managing threads
  - 🔹 Core Concepts
     - 1. Dispatch Queues
         - Queues where tasks are submitted.
         - Serial Queue → One task at a time
         - Concurrent Queue → Multiple tasks at the same time
        ```swift  
         let serialQueue = DispatchQueue(label: "com.example.serial")
         let concurrentQueue = DispatchQueue(label: "com.example.concurrent", attributes: .concurrent)
        ```
    - 2. Main Queue
       - Runs on the main thread
       - Used for UI updates
       ```swift 
      DispatchQueue.main.async {
         // Update UI here
         }
       ```
    - 3. Global Queue
      - Background thread pool managed by the system
      ```swift   
      DispatchQueue.global(qos: .background).async {
        // Background work
       }
      ```
    - 4. Sync vs Async
      - sync → waits until task finishes (blocking)
      - async → continues immediately (non-blocking)
      ```swift 
      DispatchQueue.global().async {
        print("Runs in background")
      }
      DispatchQueue.main.sync {
        print("Runs synchronously")
      }
      ```
    
### 4. What is NSOperation?
  - NSOperation is a class in Swift used for managing and executing operations concurrently.
  - 🔹 Why Use NSOperation Instead of GCD?
      - GCD is fast but low-level. NSOperation adds:
      - Task dependencies
      - Cancellation support
      - State management (ready, executing, finished) Priority control
      - KVO (Key-Value Observing) support
  - 🔹 When to Use NSOperation?
      - Use it when you need:
      - Complex workflows
      - Task dependencies
      - Fine control over execution
      - Reusable, modular tasks
  - 🔹 Key Features (Important for Interviews)
      - 1. Dependencies
           
        Control execution order:
        ```swift 
         op2.addDependency(op1)
        ```
        ➡️ op2 runs only after op1 finishes

      - 2. Cancellation
           
         ```swift    
         operation.cancel()
         ```
        Inside operation:
        
        ```swift  
        if isCancelled { return }
        ```
        
     - 3. Priority
          
        ```swift  
       operation.queuePriority = .high
        ```
        
     - 4. Max Concurrent Operations
          
        ```swift  
       queue.maxConcurrentOperationCount = 2
        ```
       ➡️ Limits number of parallel tasks

     - 5. Completion Block
          
       ```swift  
       operation.completionBlock = {
       print("Task finished")
       }
       ```
     
### 5. What is synchronous and asynchronous? 
  - `Synchronous`
        - Synchronous execution means that tasks are performed sequentially. Each task must complete before the next one starts.
  - `Asynchronous`
        - Asynchronous execution allows tasks to run concurrently, meaning that other tasks can continue running without waiting for the current task to complete.
    
### 6. What is async await?
  - Async await is a mechanism used to create and execute asynchronous functions.
  - 🧠 Key Concepts
     - 1. async
        - Marks a function as asynchronous.
        - It means the function can suspend and resume later.

     - 2. await
        - Used when calling an async function.
        - It tells Swift: “Wait here until this task finishes, but don’t block the thread.”
          
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
  - ✅ When to Use dispatch_barrier
     - 1. Reader–Writer Problem (Most Important Use Case)
        - Use it when:
        - Multiple threads can read simultaneously
        - But writes must be exclusive
        - 👉 Example: Shared cache, dictionary, array

        ```swift
       let queue = DispatchQueue(label: "com.example.concurrent", attributes: .concurrent)
       var data: [String] = []
        
       // Read (can run concurrently)
       queue.async {
         print(data)
       }

       // Write (must be exclusive)
       queue.async(flags: .barrier) {
        data.append("New Value")
       }
        ```
    
      ✔ Reads → parallel
      ✔ Writes → serialized (safe)

  - 2. Avoiding Race Conditions
    - When multiple threads update shared state, barrier ensures:
        - No partial writes
        - No corrupted data
          
  - 3. Custom Thread-Safe Data Structures
    - Instead of locks (NSLock), you can use:
        - Concurrent queue + barrier = cleaner design
          
  - 4. When You Want Better Performance Than Serial Queue
    - Serial queue → safe but slow (everything waits)
    - Concurrent + barrier → fast reads + safe writes
      
  - ⚠️ Important Rules
    - ❗ Works ONLY with Custom Concurrent Queues
      ```swift
      DispatchQueue(label: "queue", attributes: .concurrent)
      ```
    - 🚫 Does NOT work properly on:
       - Global queues (DispatchQueue.global())
       - Serial queues

    - ❗ async vs sync
      - dispatch_barrier_async → preferred (non-blocking)
      - dispatch_barrier_sync → blocks current thread (use carefully)
        
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
      - `Summary of Benefits`
     - Prevents race conditions by allowing only a controlled number of threads to access critical sections.
     - Maintains thread safety, particularly when dealing with shared data
  ```swift
     let semaphore = DispatchSemaphore(value: 1)
func performTask(_ inputValue: Int) {
    print("Task \(inputValue) is wait for access")
    semaphore.wait()
    print("Task \(inputValue) is through resouce")
    sleep(2)
    print("Task \(inputValue) is done")
    semaphore.signal()
}

DispatchQueue.global().async {
    performTask(1)
}
DispatchQueue.global().async {
    performTask(2)
}
DispatchQueue.global().async {
    performTask(3)
}

  ```
   
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
