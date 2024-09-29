## iOS Developers Interview UITableView Questions

### 1. What are table view dataSource methods?
  - cellForRowAtIndexPath
  - numberOfRowInSection
  - titleForHeaderInSection
  - titleForFooterInSection
  - canEditRowAtIndexPath
  - canMoveRowAtIndexPath

### 2. What are table view delegate methods ?
   - willSelectRowAtIndexPath
   - didSelectRowAtIndexPath
   - hightForRowAtIndexPath
   - willDisplayCell:forRowAtIndexPath
   - hightForHeaderInSection
   - hightForFooterInSection

### 3. Why we are use reuse identifier in table view cell?
  - A string identifying the cell object to be reused. This parameter must not be nil.

### 4. How to reload tableview without using reload method?

### 5. What is the difference between delegate and datasouce in swift?
  - `Delegate`:
      - A delegate is responsible for handling actions or events triggered by the user or the system.
      - Methods in the delegate protocol usually begin with phrases like didSelect, willDisplay, didEndDisplaying, etc.
        
  - `Data Source`:
      - A data source is responsible for providing data to populate a view, like a table view or collection view.
      - Methods in the data source protocol usually answer questions about the data. For example, in a UITableView, the data source will provide the number of rows and the data for each cell.
   
        
