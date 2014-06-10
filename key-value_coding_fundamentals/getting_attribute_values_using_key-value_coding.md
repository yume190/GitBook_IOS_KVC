# Getting Attribute Values Using Key-Value Coding
---

The method valueForKey: returns the value for the specified key, relative to the receiver. If there is no accessor or instance variable for the specified key, then the receiver sends itself a valueForUndefinedKey: message. The default implementation of valueForUndefinedKey: raises an NSUndefinedKeyException; subclasses can override this behavior.

Similarly, valueForKeyPath: returns the value for the specified key path, relative to the receiver. Any object in the key path sequence that is not key-value coding compliant for the appropriate key receives a valueForUndefinedKey: message.

The method dictionaryWithValuesForKeys: retrieves the values for an array of keys relative to the receiver. The returned NSDictionary contains values for all the keys in the array.

> Note: Collection objects, such as `NSArray`, `NSSet`, and `NSDictionary`, can’t contain `nil` as a value. Instead, you represent `nil` values using a special object, `NSNull`. `NSNull` provides a single instance that represents the nil value for object properties. The default implementations of dictionaryWithValuesForKeys: and `setValuesForKeysWithDictionary:` translates between `NSNull` and nil automatically, so your objects don’t have to explicitly test for `NSNull` values.

When a value is returned for a key path that contains a key for a to-many property, and that key is not the last key in the path, the returned value is a collection containing all the values for the keys to the right of the to-many key. For example, requesting the value of the key path transactions.payee returns an array containing all the payee objects, for all the transactions. This also works for multiple arrays in the key path. The key path accounts.transactions.payee would return an array with all the payee objects, for all the transactions, in all the accounts.

