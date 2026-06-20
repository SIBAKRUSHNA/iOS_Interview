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
