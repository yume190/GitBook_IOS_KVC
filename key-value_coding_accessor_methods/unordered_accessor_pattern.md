# Unordered Accessor Pattern
---

The unordered accessor methods provide a mechanism for accessing and mutating objects in an unordered relationship. Typically, this relationship is an instance of NSSet or NSMutableSet. However, by implementing these accessors, any class can by used to model the relationship and be manipulated using key-value coding just as if it was an instance of NSSet.

Getter Unordered Accessors

The getter variations of the unordered accessor methods provide simple access to the relationship data. The methods return the number of objects in the collection, an enumerator to iterate over the collection objects, and a method to compare an object with the contents of the collection to see if it is already present.

Note: It’s rare to have to implement the getter variations of the unordered accessors. To-many unordered relationships are most often modeled using instance of NSSet or a subclass. In that case the key-value coding will, if it doesn’t find these accessor patterns for the property, directly access the set. Typically, you only implement these methods if you are using a custom collection class that needs to be accessed as if it was a set.
In order to support read-only access to an unordered to-many relationship, you would implement the following methods:

-countOf<Key>. Required. This method corresponds to the NSSet method count.
-enumeratorOf<Key>. Required. Corresponds to the NSSet method objectEnumerator.
-memberOf<Key>:. Required. This method is the equivalent of the NSSet method member:
Listing 10 shows simple implementations of the necessary getter accessors that simply pass the responsibilities to the transactions property.

Listing 10  Example -countOf<Key>, -enumeratorOf<Key>, and -memberOf<Key>: accessors
- (NSUInteger)countOfTransactions {
    return [self.transactions count];
}

- (NSEnumerator *)enumeratorOfTransactions {
    return [self.transactions objectEnumerator];
}

- (Transaction *)memberOfTransactions:(Transaction *)anObject {
    return [self.transactions member:anObject];
}
The -countOf<Key> accessor implementation should simply return the number of items in the relationship. The -enumeratorOf<Key> method implementation must return an NSEnumerator instance that is used to iterate over the items in the relationship. See “Enumeration: Traversing a Collection’s Elements” in Collections Programming Topics for more information about enumerators.

The -memberOf<Key>: accessor must compare the object passed as a parameter with the contents of the collection and returns the matching object as a result, or nil if no matching object is found. Your implementation of this method may use isEqual: to compare the objects, or may compare objects in another manner. The object returned may be a different object than that tested for membership, but it should be the equivalent as far as content is concerned.

Mutable Unordered Accessors

Supporting a mutable to-many relationship with unordered accessors requires implementing additional methods. Implementing the mutable unordered accessors for your application to interact with the collection in an easy and efficient manner through the use of the array proxy returned by mutableSetValueForKey:. In addition, by implementing these methods for a to-many relationship your class will be key-value observing compliant for that property (see Key-Value Observing Programming Guide).

Note: You are strongly advised to implement these mutable accessors rather than relying on an accessor that returns a mutable array directly. The mutable accessors are much more efficient when making changes to the data in the relationship.
In order to be key-value coding complaint for a mutable unordered to-many relationship you must implement the following methods:

-add<Key>Object: or -add<Key>:. At least one of these methods must be implemented. These are analogous to the NSMutableSet method addObject:.
-remove<Key>Object: or -remove<Key>:. At least one of these methods must be implemented. These are analogous to the NSMutableSet method removeObject:.
-intersect<Key>:. Optional. Implement if benchmarking indicates that performance is an issue. It performs the equivalent action of the NSSet method intersectSet:.
The -add<Key>Object: and -add<Key>: implementations add a single item or a set of items to the relationship. You are only required to implement one of the methods. When adding a set of items to the relationship you should ensure that an equivalent object is not already present in the relationship. Listing 11 shows an example pass-through implementation for the transactions property.

Listing 11  Example -add<Key>Object: and -add<Key>: accessors
- (void)addTransactionsObject:(Transaction *)anObject {
    [self.transactions addObject:anObject];
}

- (void)addTransactions:(NSSet *)manyObjects {
    [self.transactions unionSet:manyObjects];
}
Similarly, the -remove<Key>Object: and -remove<Key>: implementations remove a single item or a set of items from the relationship. Again, implementation of only one of the methods is required. Listing 12 shows an example pass-through implementation for the transactions property.

Listing 12  Example -remove<Key>Object: and -remove<Key>: accessors
- (void)removeTransactionsObject:(Transaction *)anObject {
    [self.transactions removeObject:anObject];
}

- (void)removeTransactions:(NSSet *)manyObjects {
    [self.transactions minusSet:manyObjects];
}
If benchmarking indicates that performance improvements are required, you can also implement the -intersect<Key>: or -set<Key>: methods (see Listing 13).

The implementation of -intersect<Key>: should remove from the relationship all the objects that aren’t common to both sets. This is the equivalent of the NSMutableSet method intersectSet:.

Listing 13  Example -intersect<Key>: and -set<Key>: implementations
- (void)intersectTransactions:(NSSet *)otherObjects {
    return [self.transactions intersectSet:otherObjects];
}
