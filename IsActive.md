# IsActive Pattern

Instead of deleting items in tables add a flag that is called "IsActive". 

In all queries that you use that you need to "keep up to date", just check that you only show active values. 

Advantages:
- If you "delete" the wrong value you can easily reactivate it without affecting anything else.
- You have the possibility to access/show "old" values if you referenced them.
