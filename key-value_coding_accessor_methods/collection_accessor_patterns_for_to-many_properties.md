# Collection Accessor Patterns for To-Many Properties
---
Although your application can implement accessor methods for to-many relationship properties using the -<key> and -set<Key>: accessor forms, you should typically only use those to create the collection object. For manipulating the contents of the collection it is best practice to implement the additional accessor methods referred to as the collection accessor methods. You then use the collection accessor methods, or a mutable collection proxy returned by mutableArrayValueForKey: or mutableSetValueForKey:.

Implementing the collection accessor methods, instead of, or in addition to, the basic getter for the relationship, can have many advantages:

Performance can be increased in the case of mutable to-many relationships, often significantly.
To-many relationships can be modeled with classes other than NSArray or NSSet by implementing the appropriate collection accessors. Implementing collection accessor methods for a property makes that property indistinguishable from an array or set when using key-value coding methods.
You can use the collection accessor methods directly to make modifications to the collection in a key-value observing compliant way. See Key-Value Observing Programming Guide for more information on key-value observing.
There are two variations of collection accessors: indexed accessors for ordered to-many relationships (typically represented by NSArray) and unordered accessors for relationships that don’t require an order to the members (represented by NSSet).

