# Entity with validity period that can exist in parallel

Examples : Teams, Documents

## base table structure

```sql
CREATE TABLE Team (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  
  [Name] VARCHAR(200) NOT NULL,
  ValidFrom DATETIME NOT NULL,
  ValidUntil DATETIME,
  
  IsActive BIT NOT NULL DEFAULT 1
)
```

## t-sql: which elements are active "at the given moment"

Use a table valued function like so:

```sql
CREATE FUNCTION dbo.TeamsAtPointInTime(@PointInTime DATETIME)
RETURNS @Result TABLE (
  ... all the columns of the table but allowing NULL all the time ...
  Id INT,
  [Name] VARCHAR(200),
  ...
)
AS
BEGIN
  /*
    This is a list of active teams at a certain point in time
  */
  SELECT Id, Name, ValidFrom, ValidUntil, IsActive
    FROM Team
   WHERE IsActive = 1
     AND @PointInTime BETWEEN ValidFrom AND ISNULL(ValidUntil, @PointInTime)

  RETURN
END
```

- Teams that are "inactive" (IsActive = 0) will not be listed. They are "deleted" and thus invisible.
- Teams that are not existing yet are not listed.
- Teams that do not have a value in ValidUntil are always listed after "ValidFrom"
- Teams that have a ValidUntil DateTime set are only listed until the point in time lies after the value.


