
### 1. What is Combine?
The Combine framework provides a declarative Swift API for processing values over time. Combine is Apple's reactive programming framework introduced in iOS 13.

It helps handle:
  - Asynchronous operations
  - API calls
  - Notifications
  - User events
  - Data binding

Instead of callbacks and delegates, Combine uses Publishers and Subscribers.

### 2. Combine Framework - Deep Interview Notes

## Why Combine?

Before Combine, asynchronous tasks were handled using:

* Completion Handlers
* Delegates
* NotificationCenter
* KVO (Key Value Observing)

Example:

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

Problems:

* Callback Hell
* Hard to chain multiple API calls
* Difficult error handling
* Difficult testing

Combine solves these problems using a reactive programming approach.

---

# Reactive Programming

Reactive Programming means:

"React to changes in data automatically."

Example:

User enters username → validation runs automatically → button state updates automatically.

Instead of manually updating every component, data changes flow through a stream.

Think of Combine as a pipeline:

Data Source → Operators → Subscriber

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

# Combine Architecture

Three main components:

```text
Publisher
    ↓
Subscription
    ↓
Subscriber
```

## Publisher

Publisher produces values over time.

Generic definition:

```swift
Publisher<Output, Failure>
```

Example:

```swift
Just("Hello")
```

Output = String

Failure = Never

Meaning:

"This publisher emits one String and never fails."

---

## Subscriber

Receives values from Publisher.

Example:

```swift
Just("Hello")
    .sink { value in
        print(value)
    }
```

Flow:

```text
Publisher → Subscriber
Hello       Print
```

---

# Subscription Lifecycle

When Subscriber attaches:

```swift
publisher.sink { }
```

Steps:

1. Subscriber subscribes
2. Subscription created
3. Subscriber requests demand
4. Publisher emits values
5. Completion received

```text
Subscriber
    ↓ subscribe
Publisher
    ↓
Subscription
    ↓
Values
```

This lifecycle is a favorite interview question.

---
### 3. What is a Publisher in Combine?
A Publisher is the core component of the Combine framework that produces and emits values over time. It can send:
  - Values (zero or more)
  - Completion event (finished successfully)
  - Failure event (error)

Think of a Publisher as a data source that broadcasts information to interested subscribers.

### 4. What is a Subscriber in Combine?
A Subscriber is a component in Combine that receives values from a Publisher.
It acts as the consumer in the Publisher–Subscriber pattern.

  - Publisher → Subscriber

The Publisher produces data, and the Subscriber receives and processes it.

### 5. What is a sink and how is it used?
In Combine, sink is a subscriber used to receive values and completion events from a publisher.
It is one of the simplest ways to subscribe to a publisher.
## Syntax
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
### 6. 1. Built-in Publishers
These publishers are provided by Combine or Swift’s standard library to handle common tasks.

- Just
  - Emits a single value immediately and then completes.

## Example:
```swift
let publisher = Just("Hello, Combine!")
```

- Future
  - Produces a single result (success or failure) at some point in the future. Often used for asynchronous tasks.
## Example:
```swift
let publisher = Future<String, Error> { promise in
    DispatchQueue.global().asyncAfter(deadline: .now() + 2) {
        promise(.success("Async Value"))
    }
}
```
- PassthroughSubject
  - Allows manual publishing of values and completion events. Often used to bridge imperative code with Combine.
## Example:

```swift
let subject = PassthroughSubject<Int, Never>()
subject.send(1)
subject.send(completion: .finished)
```
- CurrentValueSubject
  - Similar to PassthroughSubject, but it keeps track of its most recent value and can replay it to new subscribers.
## Example:
```swift
let subject = CurrentValueSubject<Int, Never>(10)
subject.send(20)
```
- Empty
  - Emits no values and completes immediately or optionally never completes.
## Example:
```swift
let publisher = Empty<Int, Never>()
```
- Deferred
  - Creates a publisher that waits until a subscriber subscribes before creating and delivering a publisher.
## Example:
```swift
let publisher = Deferred {
    Just("Deferred Value")
}
```
- Timer
  - Emits values on a schedule, often used for periodic updates.
## Example:
```swift
let publisher = Timer.publish(every: 1.0, on: .main, in: .default).autoconnect()
```
- Operators as Publishers
  - Operators like CombineLatest, Map, and FlatMap can also create new publishers by transforming or combining existing ones.
