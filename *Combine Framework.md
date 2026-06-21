# Combine Framework - Complete Interview Notes

## 1. What is Combine?

The **Combine** framework provides a declarative Swift API for processing values over time. It is Apple's reactive programming framework introduced in **iOS 13**.

Combine helps handle:

* Asynchronous operations
* API calls
* Notifications
* User events
* Data binding

Instead of callbacks and delegates, Combine uses **Publishers** and **Subscribers**.

---
<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 07_37_18 PM" src="https://github.com/user-attachments/assets/07edc75f-dc4b-47ae-9295-858dd1317a10" />



# 2. Why Combine?

Before Combine, asynchronous tasks were commonly handled using:

* Completion Handlers
* Delegates
* NotificationCenter
* KVO (Key-Value Observing)

### Example

```swift
fetchUsers { result in
    switch result {
    case .success(let users):
        updateUI(users)
    case .failure(let error):
        showError(error)
    }
}
```

### Problems

* Callback Hell
* Hard to chain multiple API calls
* Difficult error handling
* Difficult testing
* Hard to maintain complex async flows

Combine solves these problems using a **reactive programming** approach.

---

# 3. Reactive Programming

Reactive Programming means:

> React to changes in data automatically.

### Example Flow

```text
User Input
     ↓
Validation
     ↓
Button State
     ↓
UI Update
```

Instead of manually updating every component, data changes flow through a stream.

### Combine Pipeline

```text
Data Source
     ↓
Publisher
     ↓
Operators
     ↓
Subscriber
```

Example:

```text
API
 ↓
Publisher
 ↓
map()
 ↓
filter()
 ↓
sink()
```

---

# 4. Combine Architecture

Combine consists of three main components:

```text
Publisher
    ↓
Subscription
    ↓
Subscriber
```

---

## Publisher

A Publisher produces values over time.

### Generic Definition

```swift
Publisher<Output, Failure>
```

### Example

```swift
Just("Hello")
```

### Meaning

```swift
Output = String
Failure = Never
```

This publisher emits a single String value and never fails.

---

## Subscriber

A Subscriber receives values from a Publisher.

### Example

```swift
Just("Hello")
    .sink { value in
        print(value)
    }
```

### Flow

```text
Publisher  →  Subscriber
 Hello     →    Print
```

---

## Subscription

A Subscription connects a Publisher and Subscriber.

It manages:

* Data flow
* Demand requests
* Cancellation

---

# 5. Subscription Lifecycle

When a Subscriber attaches to a Publisher:

```swift
publisher.sink { _ in }
```

### Steps

1. Subscriber subscribes
2. Subscription is created
3. Subscriber requests demand
4. Publisher emits values
5. Completion event is sent

### Lifecycle Diagram

```text
Subscriber
      ↓
  Subscribe
      ↓
 Publisher
      ↓
 Subscription
      ↓
    Values
      ↓
 Completion
```

⚠️ This is a very common interview question.

---

# 6. What is a Publisher?

A Publisher is the core component of Combine that produces and emits values over time.

A Publisher can send:

* Zero or more values
* Completion event
* Failure event

### Example

```swift
Just("Hello Combine")
```

Think of a Publisher as a data source that broadcasts information to interested subscribers.

---
<img width="1536" height="1024" alt="ChatGPT Image Jun 22, 2026, 01_37_20 AM" src="https://github.com/user-attachments/assets/6545dbd0-55b0-485f-b8d2-bd624b3a6bc9" />


# 7. What is a Subscriber?

A Subscriber is a component that receives values from a Publisher.

### Relationship

```text
Publisher → Subscriber
```

The Publisher produces data and the Subscriber consumes it.

### Example

```swift
Just("Hello")
    .sink { value in
        print(value)
    }
```

---
<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 07_49_20 PM" src="https://github.com/user-attachments/assets/a135eff5-e7de-48c5-817a-85be229ad304" />


# 8. What is sink?

`sink` is a built-in Subscriber provided by Combine.

It allows you to receive:

* Values
* Completion events

### Syntax

```swift
publisher.sink(
    receiveCompletion: { completion in
        print(completion)
    },
    receiveValue: { value in
        print(value)
    }
)
```

### Example

```swift
Just("Hello")
    .sink(
        receiveCompletion: { print($0) },
        receiveValue: { print($0) }
    )
```

---

# 9. Built-in Publishers

## Just

Emits a single value immediately and then completes.

```swift
let publisher = Just("Hello, Combine!")
```

### Use Cases

* Mock data
* Unit testing
* Default values

---

## Future

Produces a single success or failure value in the future.

```swift
let publisher = Future<String, Error> { promise in
    DispatchQueue.global().asyncAfter(deadline: .now() + 2) {
        promise(.success("Async Value"))
    }
}
```

### Use Cases

* API requests
* Database operations
* Async tasks

---

## PassthroughSubject

Allows manual publishing of values.

```swift
let subject = PassthroughSubject<Int, Never>()

subject.send(1)
subject.send(2)
subject.send(completion: .finished)
```

### Characteristics

* No stored value
* Sends only future values

---

## CurrentValueSubject

Stores the latest value and replays it to new subscribers.

```swift
let subject = CurrentValueSubject<Int, Never>(10)

subject.send(20)
```

### Characteristics

* Maintains current state
* New subscribers receive latest value immediately

---

## Empty

Produces no values.

```swift
let publisher = Empty<Int, Never>()
```

### Use Cases

* Testing
* Placeholder publishers

---

## Deferred

Creates a publisher only when someone subscribes.

```swift
let publisher = Deferred {
    Just("Deferred Value")
}
```

### Benefit

Execution is delayed until subscription time.

---

## Timer Publisher

Emits values periodically.

```swift
let publisher = Timer.publish(
    every: 1.0,
    on: .main,
    in: .default
)
.autoconnect()
```

### Use Cases

* Countdowns
* Polling
* Auto refresh

---

## Operators as Publishers

Operators create new publishers.

Examples:

* map
* filter
* flatMap
* combineLatest
* merge
* zip

```swift
Just(10)
    .map { $0 * 2 }
```

---

# 10. System-Provided Publishers

## NotificationCenter Publisher

Publishes system notifications.

```swift
NotificationCenter.default.publisher(
    for: UIApplication.didEnterBackgroundNotification
)
```

### Use Cases

* App lifecycle events
* Custom notifications

---

## KVO Publisher

Observes property changes using Key-Value Observing.

```swift
myObject.publisher(for: \.propertyName)
```

---

## @Published Property Wrapper

SwiftUI automatically creates publishers.

```swift
class ViewModel: ObservableObject {

    @Published var value: Int = 0

}
```

Whenever `value` changes, subscribers receive updates.

---

# 11. Custom Publishers

You can create your own Publisher by conforming to the Publisher protocol.

### Example

```swift
struct MyPublisher: Publisher {

    typealias Output = Int
    typealias Failure = Never

    func receive<S>(subscriber: S)
    where S: Subscriber,
          Failure == S.Failure,
          Output == S.Input {

        subscriber.receive(
            subscription: Subscriptions.empty
        )
    }
}
```

### Interview Point

Custom Publishers are useful when integrating legacy APIs or creating specialized data streams.

---

# 12. Built-in Subscribers

Combine provides two commonly used subscribers.

---

## sink

Handles values and completion using closures.

```swift
Just("Hello")
    .sink { value in
        print(value)
    }
```

---

## assign

Automatically assigns emitted values to an object's property.

```swift
class MyObject {
    var value = ""
}

let myObject = MyObject()

Just("Updated Value")
    .assign(to: \.value, on: myObject)
```

### Use Cases

* MVVM binding
* UI updates

---

# 13. Custom Subscribers

You can create your own Subscriber by conforming to the Subscriber protocol.

### Example

```swift
struct MySubscriber: Subscriber {

    typealias Input = String
    typealias Failure = Never

    func receive(subscription: Subscription) {
        subscription.request(.unlimited)
    }

    func receive(_ input: String) -> Subscribers.Demand {
        print("Received: \(input)")
        return .none
    }

    func receive(
        completion: Subscribers.Completion<Never>
    ) {
        print("Completed")
    }
}
```
# 14. What is the role of AnyCancellable in Combine?
AnyCancellable is an object that keeps a Combine subscription alive.

If the AnyCancellable object is released from memory, the subscription is automatically cancelled.

## Why Do We Need It?

When you subscribe to a publisher using sink(), Combine returns an AnyCancellable.
```swift
let cancellable = publisher.sink { value in
    print(value)
}
```

If you don't store cancellable, the subscription may be cancelled immediately.

## Simple Example
```swift
import Combine

let publisher = Just("Hello Combine")

let cancellable = publisher.sink { value in
    print(value)
}
```
## Output
```swift
Hello Combine
```
Here, cancellable keeps the subscription active.

<img width="1536" height="1024" alt="ChatGPT Image Jun 21, 2026, 07_22_32 PM" src="https://github.com/user-attachments/assets/9acc1377-3c73-4ddd-8166-34eac5c9a520" />


# 15. Just vs Future vs PassthroughSubject in Combine

## Overview

`Just`, `Future`, and `PassthroughSubject` are all publishers in Apple's Combine framework, but they are designed for different use cases.

| Publisher            | Emits              | Async | Can Fail       | Manual Emission |
| -------------------- | ------------------ | ----- | -------------- | --------------- |
| `Just`               | One value          | ❌ No  | ❌ No (`Never`) | ❌ No            |
| `Future`             | One value or error | ✅ Yes | ✅ Yes          | ❌ No            |
| `PassthroughSubject` | Multiple values    | ✅ Yes | ✅ Yes          | ✅ Yes           |

---

## 1. Just

### What is it?

`Just` publishes a single value immediately and then finishes.

### Example

```swift
import Combine

let publisher = Just("Hello Combine")

publisher
    .sink { value in
        print(value)
    }
```

### Output

```text
Hello Combine
```

### Lifecycle

```text
Just
 ↓
Value
 ↓
Finished
```

### Use Cases

* Mock data
* Unit testing
* Default values
* Immediate value publishing

### Key Points

* Emits exactly one value.
* Completes immediately.
* Cannot fail (`Failure = Never`).

---

## 2. Future

### What is it?

`Future` publishes a single value or error at some point in the future.

### Example

```swift
import Combine

func fetchData() -> Future<String, Error> {
    Future { promise in
        DispatchQueue.global().asyncAfter(deadline: .now() + 2) {
            promise(.success("Data Loaded"))
        }
    }
}
```

### Subscription

```swift
fetchData()
    .sink(
        receiveCompletion: { print($0) },
        receiveValue: { print($0) }
    )
```

### Output

```text
Data Loaded
finished
```

### Lifecycle

```text
Future
 ↓
Async Work
 ↓
Success / Failure
 ↓
Finished
```

### Use Cases

* API calls
* Database operations
* File loading
* One-time asynchronous tasks

### Key Points

* Emits only one result.
* Can emit success or failure.
* Completes automatically after publishing.

---

## 3. PassthroughSubject

### What is it?

`PassthroughSubject` allows values to be manually pushed to subscribers.

### Example

```swift
import Combine

let subject = PassthroughSubject<String, Never>()

subject
    .sink { value in
        print(value)
    }

subject.send("First")
subject.send("Second")
subject.send("Third")
```

### Output

```text
First
Second
Third
```

### Completion

```swift
subject.send(completion: .finished)
```

### Lifecycle

```text
PassthroughSubject
 ↓
send("First")
 ↓
send("Second")
 ↓
send("Third")
 ↓
Finished (Optional)
```

### Use Cases

* Button taps
* User actions
* Notifications
* Event broadcasting
* View ↔ ViewModel communication

### Key Points

* Can emit multiple values.
* Values are sent manually using `send()`.
* Supports completion and failure events.

---

## Real-World Examples

### Just

```swift
let usernamePublisher = Just("Siba")
```

Use when data is already available.

### Future

```swift
func login() -> Future<User, Error>
```

Use for a single asynchronous operation.

### PassthroughSubject

```swift
let buttonTap = PassthroughSubject<Void, Never>()

buttonTap.send(())
```

Use for repeated user events.

---

## Interview Answer

### What is the difference between Just, Future, and PassthroughSubject?

* **Just** emits one value immediately and then completes.
* **Future** emits one value or error asynchronously and then completes.
* **PassthroughSubject** allows manual emission of multiple values over time and is commonly used for events and notifications.

---

## Quick Revision

```text
Just                → One value now
Future              → One value later
PassthroughSubject  → Many values whenever needed
```

### Memory Trick

```text
Just       = Present
Future     = Later
Subject    = Multiple Events
```
# 16. assign(to:on:) vs sink(receiveValue:)

Both `assign` and `sink` are subscribers in Combine, but they serve different purposes.

| assign(to:on:) | sink(receiveValue:) |
|---------------|--------------------|
| Updates a property automatically | Executes custom code |
| Less flexible | More flexible |
| Cannot handle completion | Can handle completion |
| Ideal for data binding | Ideal for side effects and custom logic |

## assign(to:on:)

Use when you want to bind publisher output directly to an object's property.

```swift
Just("Siba")
    .assign(to: \.name, on: user)
```

Equivalent to:

```swift
Just("Siba")
    .sink { value in
        user.name = value
    }
```

## sink(receiveValue:)

Use when you need custom actions on received values.

```swift
Just("Siba")
    .sink { value in
        print(value)
        updateUI(value)
    }
```

## Handling Completion

`sink` can receive completion events:

```swift
publisher.sink(
    receiveCompletion: { completion in
        print(completion)
    },
    receiveValue: { value in
        print(value)
    }
)
```

## When to Use?

✅ **assign** → Simple property binding

```swift
publisher.assign(to: \.text, on: label)
```

✅ **sink** → Custom logic, side effects, logging, API calls

```swift
publisher.sink { value in
    print(value)
    analytics.track(value)
}
```

### Interview Answer

> `assign(to:on:)` is a specialized subscriber used for property binding, while `sink(receiveValue:)` is a general-purpose subscriber used to execute custom code whenever values are received.

# 17. How Combine Replaces Delegation and Callbacks

Before Combine, asynchronous communication was commonly handled using **delegates** and **completion handlers (callbacks)**.

Combine provides a **reactive, declarative approach** where data is emitted by **Publishers** and consumed by **Subscribers**.

---

## 1. Traditional Callback Approach

```swift
func fetchUser(completion: @escaping (User?) -> Void) {
    apiService.getUser { user in
        completion(user)
    }
}

fetchUser { user in
    print(user?.name ?? "")
}
```

### Problems

- Nested callbacks can lead to "callback hell".
- Hard to chain multiple asynchronous operations.
- Error handling becomes scattered.
- Difficult to manage complex data flows.

---

## 2. Traditional Delegate Approach

```swift
protocol LoginDelegate: AnyObject {
    func loginDidSucceed(user: User)
}

class LoginManager {
    weak var delegate: LoginDelegate?

    func login() {
        delegate?.loginDidSucceed(user: user)
    }
}
```

### Problems

- Requires creating protocols.
- Tight coupling between objects.
- Becomes difficult when multiple listeners are needed.

---

## 3. Combine Approach

```swift
func fetchUser() -> AnyPublisher<User, Error> {
    apiService.getUserPublisher()
}

fetchUser()
    .sink(
        receiveCompletion: { completion in
            print(completion)
        },
        receiveValue: { user in
            print(user.name)
        }
    )
    .store(in: &cancellables)
```

### Benefits

- No delegate protocols.
- No completion-handler nesting.
- Easy chaining with operators.
- Built-in error handling.
- Multiple subscribers can listen to the same publisher.
- Cleaner and more readable code.

---

## Example: Delegate vs Combine

### Delegate

```swift
protocol DataDelegate: AnyObject {
    func didReceiveData(_ value: String)
}
```

### Combine

```swift
let subject = PassthroughSubject<String, Never>()

subject
    .sink { value in
        print(value)
    }
    .store(in: &cancellables)

subject.send("Hello Combine")
```

---

## Interview Answer

**How does Combine replace delegation or callbacks?**

Combine replaces delegates and callbacks by using a Publisher-Subscriber model. Instead of manually passing data through delegate methods or completion handlers, publishers emit values over time and subscribers react to those values. This results in cleaner, more maintainable, and composable asynchronous code with built-in support for error handling and data transformation.

# 18. Threading in Combine

Combine uses **Schedulers** to control where work is performed and where values are received.

## subscribe(on:)

Controls **where the publisher performs its work**.

```swift
publisher
    .subscribe(on: DispatchQueue.global())
```

✅ Used for background tasks (networking, parsing, heavy computations).

---

## receive(on:)

Controls **where the subscriber receives values**.

```swift
publisher
    .receive(on: DispatchQueue.main)
```

✅ Used for UI updates.

---

## Common Usage

```swift
publisher
    .subscribe(on: DispatchQueue.global())
    .receive(on: DispatchQueue.main)
    .sink { value in
        self.label.text = value
    }
    .store(in: &cancellables)
```

### Quick Difference

| subscribe(on:) | receive(on:) |
|---------------|--------------|
| Controls upstream work | Controls downstream delivery |
| Background processing | UI updates |
| Publisher side | Subscriber side |

### Interview Answer

> `subscribe(on:)` determines where the publisher does its work, while `receive(on:)` determines where subscribers receive values. Typically, heavy work runs on a background queue and UI updates are delivered on the main queue.

# 19. debounce vs throttle vs removeDuplicates

These are Combine operators used to control how frequently values are emitted.

---

## 1. debounce

Waits for a pause in incoming events before emitting the latest value.

### Example

```swift
searchTextPublisher
    .debounce(for: .milliseconds(500), scheduler: RunLoop.main)
```

### Use Case

- Search bars
- User typing input
- Avoid excessive API calls

### Timeline

```text
Input:  H -- He -- Hel -- Hell -- Hello
Output: ------------------------ Hello
```

Only the final value is emitted after the user stops typing.

---

## 2. throttle

Limits how often values are emitted.

### Example

```swift
publisher
    .throttle(for: .seconds(1),
              scheduler: RunLoop.main,
              latest: true)
```

### Use Case

- Button taps
- Scroll events
- Location updates

### Timeline

```text
Input:  A B C D E F
Output: A ----- D ----- F
```

Only one value is emitted per time interval.

---

## 3. removeDuplicates

Prevents consecutive duplicate values from being emitted.

### Example

```swift
publisher
    .removeDuplicates()
```

### Timeline

```text
Input:  A A B B C C C D
Output: A B C D
```

### Use Case

- Search text
- State updates
- Avoid unnecessary UI refreshes

---

## Common Search Example

```swift
searchTextPublisher
    .removeDuplicates()
    .debounce(for: .milliseconds(500), scheduler: RunLoop.main)
    .sink { text in
        searchAPI(text)
    }
    .store(in: &cancellables)
```

### What Happens?

1. Duplicate text is ignored.
2. Waits until the user stops typing for 500 ms.
3. Makes a single API call.

---

## Quick Difference

| Operator | Purpose |
|-----------|----------|
| `debounce` | Wait for inactivity before emitting |
| `throttle` | Limit emission frequency |
| `removeDuplicates` | Ignore consecutive duplicate values |

### Interview Answer

> `debounce` waits for a pause before emitting the latest value, `throttle` limits how often values are emitted within a time interval, and `removeDuplicates` prevents consecutive duplicate values from being published.

# 20. Operators

<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 07_04_24 PM" src="https://github.com/user-attachments/assets/aae32e64-a6b7-4d33-8a9f-c095d15ee792" />
