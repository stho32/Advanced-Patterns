# Entity

An entity is a table that holds some data. 

Normally you will need a table and some user interface. You will want to know who saved what and when and at least who changed "it" last.

## base table structure

```sql
CREATE TABLE Apple (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  RecordedAt DATETIME NOT NULL DEFAULT GETDATE(),
  RecordedBy INT NOT NULL REFERENCES ...,
  LastChangedAt DATETIME NOT NULL DEFAULT GETDATE(),
  LastChangedBy INT NOT NULL REFERENCES ...,
  ...
  IsActive BIT NOT NULL DEFAULT 1
)
```

Please note: 
- the tables name is singular

## implementing in c#

- interface for the entity that is read only
- poco-class with parameterized constructor
- an interface for the repository
- an repository that uses the poco class internally but only returns and/or uses the interface representation of the entity

Using the interface, the hidden poco and returning only arrays you implement immutability, which is most of the time a good thing considering the 
mess that is usually following mutability. You can effectivly control every usage of the data this way and the compiler will help you with every
change you make.

The interfaces will also allow you to implement tests more efficiently. Instead of using mock frameworks simply use your interfaces to implement mocks.
That is straight forward and you can easily see what you do.

