# Predecessor and IsActive (aka "never update, only save")

Using this pattern you always have a revision history of the entity.

## table structure

```sql
CREATE TABLE Entity (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  Timestamp DATETIME NOT NULL DEFAULT GETDATE(),
  ...
  Predecessor INT NOT NULL REFERENCES Entity(Id),
  IsActive BIT NOT NULL DEFAULT 1
)
```

When saving set the predecessor to the record of the last version and set the last versions IsActive-flag to 0.
This way you have always a clean list of everything that is "cool now". 

If you add a timestamp and maybe a reference to the employee that has written the data record to the database you have a complete history of what was 
changed by whom and when which gives you the opportunity of being very accurate when you are playing detective or suddenly need to create
a statistic of some sort that reaches back a few years.
