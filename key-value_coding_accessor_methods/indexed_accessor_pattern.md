# Indexed Accessor Pattern
---

The indexed accessor methods define a mechanism for counting, retrieving, adding, and replacing objects in an ordered relationship. Typically this relationship is an instance of NSArray or NSMutableArray; however, any object can implement these methods and be manipulated just as if it was an array. You are not restricted to simply implementing these methods, you can also invoke them as well to interact directly with objects in the relationship.

There are indexed accessors which return data from the collection (the getter variation) and mutable accessors that provide an interface for mutableArrayValueForKey: to modify the collection.

Getter Indexed Accessors

In order to support read-only access to an ordered to-many relationship, implement the following methods:

 * `-countOf<Key>`. Required. This is the analogous to the NSArray primitive method count.

 * `-objectIn<Key>AtIndex:` or `-<key>AtIndexes:`. One of these methods must be implemented. They correspond to the NSArray methods `objectAtIndex:` and `objectsAtIndexes:`.

 * `-get<Key>:range:`. Implementing this method is optional, but offers additional performance gains. This method corresponds to the NSArray method `getObjects:range:`.

An implementation of the `-countOf<Key>` method simply returns the number of objects in the to-many relationship as an NSUInteger. The code fragment in Listing 4 illustrates the `-countOf<Key>` implementation for the to-many relationship property employees.

__Listing 4__  Example `-count<Key>` implementation
    - (NSUInteger)countOfEmployees {
        return [self.employees count];
    }
The `-objectIn<Key>AtIndex:` method returns the object at the specified index in the to-many relationship. The `-<key>AtIndexes:` accessor form returns an array of objects at the indexes specified by the NSIndexSet parameter. Only one of these two methods must be implemented.

The code fragment in Listing 5 shows `-objectIn<Key>AtIndex:` and `-<key>AtIndexes:` implementations for a to-many relationship property employees.

__Listing 5__  Example `-objectIn<Key>AtIndex:` and `-<key>AtIndexes:` implementations
    - (id)objectInEmployeesAtIndex:(NSUInteger)index {
        return [employees objectAtIndex:index];
    }

    - (NSArray *)employeesAtIndexes:(NSIndexSet *)indexes {
        return [self.employees objectsAtIndexes:indexes];
    }
If benchmarking indicates that performance improvements are required, you can also implement -get<Key>:range:. Your implementation of this accessor should return in the buffer given as the first parameter the objects that fall within the range specified by the second parameter.

Listing 6 shows an example implementation of the -get<Key>:range: accessor pattern for the to-many employees property.

__Listing 6__  Example `-get<Key>:range:` implementation
    - (void)getEmployees:(Employee * __unsafe_unretained *)buffer range:(NSRange)inRange {
        // Return the objects in the specified range in the provided buffer.
        // For example, if the employees were stored in an underlying NSArray
        [self.employees getObjects:buffer range:inRange];
    }
Mutable Indexed Accessors

Supporting a mutable to-many relationship with indexed accessors requires implementing additional methods. Implementing the mutable indexed accessors allow your application to interact with the indexed collection in an easy and efficient manner by using the array proxy returned by mutableArrayValueForKey:. In addition, by implementing these methods for a to-many relationship your class will be key-value observing compliant for that property (see Key-Value Observing Programming Guide).

Note: You are strongly advised to implement these mutable accessors rather than relying on an accessor that returns a mutable set directly. The mutable accessors are much more efficient when making changes to the data in the relationship.
In order to be key-value coding compliant for a mutable ordered to-many relationship you must implement the following methods:

-insertObject:in<Key>AtIndex: or -insert<Key>:atIndexes:. At least one of these methods must be implemented. These are analogous to the NSMutableArray methods insertObject:atIndex: and insertObjects:atIndexes:.
-removeObjectFrom<Key>AtIndex: or -remove<Key>AtIndexes:. At least one of these methods must be implemented. These methods correspond to the NSMutableArray methods removeObjectAtIndex: and removeObjectsAtIndexes: respectively.
-replaceObjectIn<Key>AtIndex:withObject: or -replace<Key>AtIndexes:with<Key>:. Optional. Implement if benchmarking indicates that performance is an issue.
The -insertObject:in<Key>AtIndex: method is passed the object to insert, and an NSUInteger that specifies the index where it should be inserted. The -insert<Key>:atIndexes: method inserts an array of objects into the collection at the indices specified by the passed NSIndexSet. You are only required to implement one of these two methods.

Listing 7 shows sample implementations of both insert accessors for the to-many employee property.

Listing 7  Example -insertObject:in<Key>AtIndex: and -insert<Key>:atIndexes: accessors

    - (void)insertObject:(Employee *)employee inEmployeesAtIndex:(NSUInteger)index {
        [self.employees insertObject:employee atIndex:index];
        return;
    }

    - (void)insertEmployees:(NSArray *)employeeArray atIndexes:(NSIndexSet *)indexes {
        [self.employees insertObjects:employeeArray atIndexes:indexes];
        return;
    }

The -removeObjectFrom<Key>AtIndex: method is passed an NSUInteger value specifying the index of the object to be removed from the relationship. The -remove<Key>AtIndexes: is passed an NSIndexSet specifying the indexes of the objects to be removed from the relationship. Again, you are only required to implement one of these methods.

Listing 8 shows sample implementations of -removeObjectFrom<Key>AtIndex: and -remove<Key>AtIndexes: implementations for the to-many employee property.

Listing 8  Example -removeObjectFrom<Key>AtIndex: and -remove<Key>AtIndexes: accessors
    - (void)removeObjectFromEmployeesAtIndex:(NSUInteger)index {
        [self.employees removeObjectAtIndex:index];
    }

    - (void)removeEmployeesAtIndexes:(NSIndexSet *)indexes {
        [self.employees removeObjectsAtIndexes:indexes];
    }
If benchmarking indicates that performance improvements are required, you can also implement one or both of the optional replace accessors. Your implementation of either -replaceObjectIn<Key>AtIndex:withObject: or -replace<Key>AtIndexes:with<Key>: are called when an object is replaced in a collection, rather than doing a remove and then insert.

Listing 9 shows sample implementations of -replaceObjectIn<Key>AtIndex:withObject: and -replace<Key>AtIndexes:with<Key>: implementations for the to-many employee property.

Listing 9  Example -replaceObjectIn<Key>AtIndex:withObject: and -replace<Key>AtIndexes:with<Key>: accessors
- (void)replaceObjectInEmployeesAtIndex:(NSUInteger)index
                             withObject:(id)anObject {

    [self.employees replaceObjectAtIndex:index withObject:anObject];
}

- (void)replaceEmployeesAtIndexes:(NSIndexSet *)indexes
                    withEmployees:(NSArray *)employeeArray {

    [self.employees replaceObjectsAtIndexes:indexes withObjects:employeeArray];
}
