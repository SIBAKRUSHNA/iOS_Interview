## iOS Developers Interview Core Data Questions

### 1. What is core Data migration?
- Steps for Core Data Migration
- `Version the Data Model`:
    - Go to your .xcdatamodeld file, click on "Editor" -> "Add Model Version."
    - Create a new version of the data model (e.g., ModelV2).
    - Make changes in the new version while keeping the old one as a fallback.
- `Set the Current Version`:
    - After creating a new version, make sure to set the newly created one (e.g., ModelV2) as the current data model version from the File Inspector.
- `Lightweight Migration Setup`:
    - If the migration is lightweight, Core Data will automatically handle it. Ensure the following options are set in your persistent store coordinator

### 2.

### 3.

### 4.
