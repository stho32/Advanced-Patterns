# Flexible/Complex process

A process that contains a tree of possible steps and / or loops of some kind. It might as well be endless. 

## base sql structure

```sql
/*
  Each entry in this table represents one process that is running or completed.
*/
CREATE TABLE HaveComplexLunchProcess (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  ...
  Common data that is shared within the process but is only available once
  ...
  CurrentState ... 
  IsCompleted ...
  ...
  IsActive BIT NOT NULL DEFAULT 1
)

/*
  This is a table that starts as an enumeration but might grow
  describing the possible states of the workflow.
*/
CREATE TABLE HaveComplexLunchProcessState (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  ...
  IsActive BIT NOT NULL DEFAULT 1
)

/* Another optional table that will reference a state
   and describe where you can go from there...
*/
CREATE TABLE HaveComplexLunchProcessStateOption (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  ...
  IsActive BIT NOT NULL DEFAULT 1
)

/*
  This is an optional table in which you might collect information while 
  the process is running along.
*/
CREATE TABLE HaveComplexLunchProcessContext (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  Process INT NOT NULL REFERENCES HaveComplexLunchProcess(Id),
  ...
  [Name] VARCHAR(200) NOT NULL DEFAULT '',
  Value VARCHAR(200) NOT NULL DEFAULT '',
  ...
  IsActive BIT NOT NULL DEFAULT 1
)

/*
  This is the log table that logs every step along the way and might as well
  collect some data. Anyways, you should not collect to much data here because 
  when you need to manipulate a running process because of strange business
  issues you might need to change data in a way that you cannot accomplish when
  you need it bound to a step in your log...
*/
CREATE TABLE HaveComplexLunchProcessLog (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  Process INT NOT NULL REFERENCES HaveComplexLunchProcess(Id),
  Timestamp DATETIME NOT NULL DEFAULT GETDATE(),
  
  ...Additional data...
  
  StepPerformedBy INT NOT NULL REFERENCE ...,
  IsActive BIT NOT NULL DEFAULT 1
)
```

