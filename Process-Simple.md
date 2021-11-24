# Simple linear process

Within a simple linear process states are all tracked within the row of a table, each table row representing one process.
Each state is at least a datetime field with a time stamp that is either NULL (state not reached yet) or a time stamp of the time, when the state was reached.
Fields that are needed to be filled with additional information are simply added to the table as well.

## base sql structure

```sql
CREATE TABLE HaveLunch (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  ProcessStarted DATETIME NOT NULL DEFAULT GETDATE(),
  EmployeeHavingLunch INT NOT NULL REFERENCES ...,
  
  RestaurantIsChosen DATETIME,
  RestaurantIsChosenBy INT REFERENCES ...,
  Restaurant INT REFERENCES ...,
  
  FoodIsChosen DATETIME,
  FoodIsChosenBy INT REFERENCES ...,
  Food VARCHAR(MAX),
  
  ...
  
  IsActive BIT NOT NULL DEFAULT 1
)
```

