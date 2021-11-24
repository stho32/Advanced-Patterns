# Enumeration

An enumeration is a specialised entity that represents a list of states or values of which one can selected per referencing entity or reference table.

By using a separate table instead of flags within an entity you say clearly: This is a selection, you choose *one* value.
Another thing is that with time people might come around and add properties, for example they might say that certain states might be represented by an image. 
Or that one of the values is a default. That they should occur in a special order, have a different value, color or whatever.
This way you are free to add the additional properties. 

## base table structure

```sql
CREATE TABLE State (
  Id INT NOT NULL PRIMARY KEY IDENTITY,
  [Name] VARCHAR(200) NOT NULL,
  Order INT NOT NULL DEFAULT 0,
  IsActive BIT
)
```

## Usage example from an entity table

```sql
CREATE TABLE SomeEntity (
  ...
  State INT NOT NULL REFERENCES State(Id),
  ...
)
```

## Representation in C#

From C# you use this as if it was a list. Do not use `enum` because they force you to change the code when the content of the table changes. 
Do not reference special values, like ID's for certain states, in your code. 
Instead add flags to the base table structure and use them e.g. to define the "default location for usage in statistics when nothing else is given".

Use repository, interface, poco-entity .

