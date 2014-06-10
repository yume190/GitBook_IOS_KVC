# Ensuring KVC Compliance
---
In order for a class to be considered KVC compliant for a specific property, it must implement the methods required for valueForKey: and setValue:forKey: to work for that property.

Attribute and To-One Relationship Compliance

For properties that are an attribute or a to-one relationship, this requires that your class:

Implement a method named -<key>, -is<Key>, or have an instance variable <key> or _<key>.
Although key names frequently begin with a lowercase letter, KVC also supports key names that begin with an uppercase letter, such as URL.

If the property is mutable, then it should also implement -set<Key>:.
Your implementation of the -set<Key>: method should not perform validation.
Your class should implement -validate<Key>:error: if validation is appropriate for the key.
Indexed To-Many Relationship Compliance

For indexed to-many relationships, KVC compliance requires that your class:

Implement a method named -<key> that returns an array.
Or have an array instance variable named <key> or _<key>.
Or implement the method -countOf<Key> and one or both of -objectIn<Key>AtIndex: or -<key>AtIndexes:.
Optionally, you can also implement -get<Key>:range: to improve performance.
For a mutable indexed ordered to-many relationship, KVC compliance requires that your class also:

Implement one or both of the methods -insertObject:in<Key>AtIndex: or -insert<Key>:atIndexes:.
Implement one or both of the methods -removeObjectFrom<Key>AtIndex: or -remove<Key>AtIndexes:.
Optionally, you can also implement -replaceObjectIn<Key>AtIndex:withObject: or -replace<Key>AtIndexes:with<Key>: to improve performance.
Unordered To-Many Relationship Compliance

For unordered to-many relationships, KVC compliance requires that your class:

Implement a method named -<key> that returns a set.
Or have a set instance variable named <key> or _<key>.
Or implement the methods -countOf<Key>, -enumeratorOf<Key>, and -memberOf<Key>:.
For a mutable unordered to-many relationship, KVC compliance requires that your class also:

Implement one or both of the methods -add<Key>Object: or -add<Key>:.
Implement one or both of the methods -remove<Key>Object: or -remove<Key>:.
Optionally, you can also implement -intersect<Key>: and -set<Key>: to improve performance.
