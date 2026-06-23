## iOS Developers Interview Core Data Questions

<img width="1024" height="1536" alt="ChatGPT Image Jun 23, 2026, 11_44_43 PM" src="https://github.com/user-attachments/assets/9270973f-a66a-4d1c-a4eb-a6e3e417bce9" />


### What is core Data migration?
- Steps for Core Data Migration
- `Version the Data Model`:
    - Go to your .xcdatamodeld file, click on "Editor" -> "Add Model Version."
    - Create a new version of the data model (e.g., ModelV2).
    - Make changes in the new version while keeping the old one as a fallback.
- `Set the Current Version`:
    - After creating a new version, make sure to set the newly created one (e.g., ModelV2) as the current data model version from the File Inspector.
- `Lightweight Migration Setup`:
    - If the migration is lightweight, Core Data will automatically handle it. Ensure the following options are set in your persistent store coordinator

## 1. What is Core Data? ⭐⭐⭐⭐⭐

**Answer:**
Core Data is Apple's framework for managing, storing, and persisting application data. It provides object graph management, change tracking, relationships, faulting, and data persistence.

> Core Data is NOT a database. It is an Object Graph Management Framework that can use SQLite as its storage backend.

---

## 2. What are the main components of the Core Data Stack? ⭐⭐⭐⭐⭐

**Answer:**

### NSManagedObjectModel
Defines entities, attributes, and relationships.

### NSPersistentStoreCoordinator
Connects the model to the persistent store.

### NSPersistentStore
Stores data physically (SQLite, Binary, In-Memory).

### NSManagedObjectContext
Used to create, fetch, update, and delete data.

### NSPersistentContainer
Simplifies Core Data stack setup.

---

## 3. What is NSManagedObjectContext? ⭐⭐⭐⭐⭐

**Answer:**
NSManagedObjectContext is a temporary workspace where managed objects are created, fetched, updated, and deleted before being saved to the persistent store.

```swift
let context = persistentContainer.viewContext
```

---

## 4. What is NSPersistentContainer? ⭐⭐⭐⭐⭐

**Answer:**
Introduced in iOS 10, NSPersistentContainer simplifies Core Data stack creation and management.

```swift
let container = NSPersistentContainer(name: "MyApp")
container.loadPersistentStores()
```

---

## 5. How do you save data in Core Data? ⭐⭐⭐⭐⭐

```swift
let user = User(context: context)
user.name = "John"

try? context.save()
```

---

## 6. How do you fetch data from Core Data? ⭐⭐⭐⭐⭐

```swift
let request: NSFetchRequest<User> = User.fetchRequest()
let users = try? context.fetch(request)
```

---

## 7. How do you update data? ⭐⭐⭐⭐⭐

```swift
user.name = "David"
try? context.save()
```

---

## 8. How do you delete data? ⭐⭐⭐⭐⭐

```swift
context.delete(user)
try? context.save()
```

---

## 9. What is NSFetchRequest? ⭐⭐⭐⭐⭐

**Answer:**
NSFetchRequest is used to retrieve objects from Core Data.

```swift
let request = NSFetchRequest<User>(entityName: "User")
```

---

## 10. What is Faulting in Core Data? ⭐⭐⭐⭐⭐

**Answer:**
Faulting is a memory optimization technique where Core Data loads object data only when it is accessed.

### Benefits
- Reduces memory usage
- Improves performance
- Supports large datasets

---

## 11. What are Relationships in Core Data? ⭐⭐⭐⭐⭐

**Answer:**

### One-to-One
```text
User ↔ Profile
```

### One-to-Many
```text
Department → Employees
```

### Many-to-One
```text
Employees → Department
```

### Many-to-Many
```text
Students ↔ Courses
```

---

## 12. What is an Inverse Relationship? ⭐⭐⭐⭐

**Answer:**
An inverse relationship automatically keeps both sides of a relationship synchronized.

Example:

```text
Department ↔ Employee
```

When an employee is added to a department, Core Data automatically updates both relationships.

---

## 13. What is Core Data Migration? ⭐⭐⭐⭐⭐

**Answer:**
Migration is the process of updating an existing database when the data model changes.

### Types

#### Lightweight Migration
- Add attribute
- Add entity
- Rename attribute

#### Heavyweight Migration
- Complex schema changes
- Requires custom mapping model

---

## 14. What is Lightweight Migration? ⭐⭐⭐⭐⭐

```swift
description.shouldMigrateStoreAutomatically = true
description.shouldInferMappingModelAutomatically = true
```

**Answer:**
Automatically handles simple model changes without custom mapping.

---

## 15. What is Heavyweight Migration? ⭐⭐⭐⭐

**Answer:**
Used when model changes are too complex for automatic migration and require custom mapping models.

---

## 16. What are Concurrency Types in Core Data? ⭐⭐⭐⭐⭐

### Main Queue Context

```swift
.mainQueueConcurrencyType
```

Used for UI operations.

### Private Queue Context

```swift
.privateQueueConcurrencyType
```

Used for background operations.

---

## 17. Why is Core Data not Thread Safe? ⭐⭐⭐⭐

**Answer:**
Managed objects belong to a specific context and queue. Accessing them from another thread can cause crashes and data corruption.

---

## 18. How do you perform Core Data operations in the background? ⭐⭐⭐⭐⭐

```swift
persistentContainer.performBackgroundTask { context in
    // Background operations
}
```

**Answer:**
Background contexts prevent UI blocking during heavy operations.

---

## 19. What is a Parent-Child Context? ⭐⭐⭐⭐

**Answer:**
A child context saves changes to its parent context first, and then the parent saves to disk.

```swift
childContext.parent = parentContext
```

### Benefits
- Faster saves
- Better responsiveness
- Background processing

---

## 20. What is a Merge Policy? ⭐⭐⭐⭐

**Answer:**
Defines how Core Data resolves conflicts when multiple contexts modify the same object.

```swift
context.mergePolicy = NSMergeByPropertyObjectTrumpMergePolicy
```

### Common Policies

- Error
- Store Trump
- Object Trump
- Overwrite
- Rollback

---

## 21. What is NSFetchedResultsController? ⭐⭐⭐⭐⭐

**Answer:**
Monitors Core Data changes and automatically updates UITableView or UICollectionView.

```swift
let frc = NSFetchedResultsController(...)
```

---

## 22. What is Batch Delete? ⭐⭐⭐⭐

```swift
let deleteRequest = NSBatchDeleteRequest(fetchRequest: fetchRequest)
try? context.execute(deleteRequest)
```

**Answer:**
Deletes large datasets directly from SQLite without loading objects into memory.

---

## 23. What is Batch Update? ⭐⭐⭐⭐

**Answer:**
Updates multiple records directly in the persistent store without loading them into memory.

### Benefits
- Faster updates
- Lower memory usage

---

## 24. What is an Entity? ⭐⭐⭐⭐

**Answer:**
An Entity is similar to a database table.

Example:

```text
User
Employee
Product
```

---

## 25. What is an Attribute? ⭐⭐⭐⭐

**Answer:**
An Attribute is similar to a table column.

Example:

```text
User
 ├─ name
 ├─ email
 └─ age
```

---

## 26. What is ObjectID? ⭐⭐⭐⭐

**Answer:**
A unique identifier generated by Core Data for each managed object.

```swift
let id = user.objectID
```

### Advantages
- Unique
- Permanent
- Thread-safe reference

---

## 27. What is the difference between Core Data and SQLite? ⭐⭐⭐⭐⭐

| Core Data | SQLite |
|------------|---------|
| Framework | Database Engine |
| Object-Based | Table-Based |
| Faulting | No Faulting |
| Relationships | Manual |
| Change Tracking | No Tracking |

---

## 28. What is the difference between Core Data and UserDefaults? ⭐⭐⭐⭐⭐

| Core Data | UserDefaults |
|------------|-------------|
| Large Structured Data | Small Data |
| Relationships | No Relationships |
| Query Support | No Queries |
| Scalable | Limited |

---

## 29. What happens when `context.save()` is called? ⭐⭐⭐

**Answer:**

1. Context validates objects.
2. Tracks inserted, updated, and deleted objects.
3. Sends changes to Persistent Store Coordinator.
4. Data is written to SQLite.
5. Context is marked clean.

---

## 30. How do you optimize Core Data performance? ⭐⭐⭐⭐⭐

**Answer:**

### Use Predicates

```swift
request.predicate = NSPredicate(format: "age > 18")
```

### Use Fetch Limits

```swift
request.fetchLimit = 20
```

### Use Faulting

Loads data only when needed.

### Use Batch Operations

- Batch Delete
- Batch Update

### Use Background Contexts

```swift
performBackgroundTask()
```

### Fetch Only Required Fields

```swift
request.propertiesToFetch = ["name"]
```

---

# Most Asked Interview Questions

1. What is Core Data?
2. Explain Core Data Stack.
3. What is NSManagedObjectContext?
4. What is Faulting?
5. What is NSPersistentContainer?
6. Difference between Core Data and SQLite.
7. Difference between Core Data and UserDefaults.
8. What is Migration?
9. Explain Concurrency in Core Data.
10. How do you optimize Core Data performance?

> Preparing these Top 10 questions covers around 80-90% of Core Data interview discussions for 3-8 years experienced iOS Developers.
