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
  - `Synchronous` - Synchronous execution means that tasks are performed sequentially. Each task must complete before the next one starts.
  - `Asynchronous` - Asynchronous execution allows tasks to run concurrently, meaning that other tasks can continue running without waiting for the current task to complete.
    
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
  
### 9.

### 10.

### 11.

