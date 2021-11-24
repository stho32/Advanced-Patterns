# Advanced-Patterns
Notes on Advanced Software Design Patterns for database based multi tier applications in C#

These are my notes on more advanced patterns in my software development practice.
No, I am not talking Adapter, Singleton or Factory. 
I talk about design patterns and how I have learned to use them in T-SQL and C# to get a flexible system that can be extended.

## general

- [IsActive-Flag](IsActive.md)
- [Predecessor and IsActive](Predecessor-and-IsActive.md)

## data

- [Entity](Entity.md)
- [Enumeration](Enumeration.md)
- [Reference table](Reference-Table.md)

## special data

- [Entities which replace each other in/around their validity period](Entity-with-validity-period-one-active.md)
- [Entities with validity period that can exist in parallel](Entity-with-validity-period-that-can-exist-in-parallel.md)

## representing processes

- [Simple linear process](Process-Simple.md)
- [Flexible/Complex process](Process-Complex.md)
- [Flexible/Complex process that is versioned](Process-Complex-Versioned.md)
