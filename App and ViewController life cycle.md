## iOS Developers Interview App and ViewController life cycle Questions

![](https://miro.medium.com/v2/resize:fit:2000/1*09LWJWdZSuPrv15I16WYiw.png)

### 1. What is the application life cycle?
  - The application life cycle constitutes the sequence of events that occurs between the launch and termination of 
    application.
### `Delegate methods`
  - application:willFinishLaunchingWithOptions
  - application:didFinishLaunchingWithOptions
  - applicationWillEnterForeground
  - applicationDidBecomeActive
  - applicationWillResignActive
  - applicationDidEnterBackground
  - applicationWillTerminate
    
### 2. What are the application different state ?
  `Not Running`
    - Either the application is not started or is terminated by system. 
    
  `Inactive`
    - An application is running in the foreground but is not receiving any events. User interaction is not possible at this 
      time. This happens when a call or SMS is received.
      
  `Active`
    - An application is running in the foreground and receiving the events. User interaction happens only in this state.
    
  `Background`
    - An application is running in the background and executing the code.
  
  `Suspended`
    -  When it's in the background and doesn't have any pending tasks to complete.
  
### 3. What is the ViewController life cycle?
`init`
`loadView` 
        - The view controller calls this method when its view property is requested but is currently nil
        
![](https://swiftacademy.ir/images/swift-learning/other/view-controller-lifecycle.jpg)
### 4.

### 5.

### 6.

### 7.

### 8.

### 9.

### 10.

### 11.
