# Setting Attribute Values Using Key-Value Coding
---

The method setValue:forKey: sets the value of the specified key, relative to the receiver, to the provided value. The default implementation of setValue:forKey: automatically unwraps NSValue objects that represent scalars and structs and assigns them to the property. See “Scalar and Structure Support” for details on the wrapping and unwrapping semantics.

If the specified key does not exist, the receiver is sent a setValue:forUndefinedKey: message. The default implementation of setValue:forUndefinedKey: raises an NSUndefinedKeyException; however, subclasses can override this method to handle the request in a custom manner.

The method setValue:forKeyPath: behaves in a similar fashion, but it is able to handle a key path as well as a single key.

Finally, setValuesForKeysWithDictionary: sets the properties of the receiver with the values in the specified dictionary, using the dictionary keys to identify the properties. The default implementation invokes setValue:forKey: for each key-value pair, substituting nil for NSNull objects as required.

One additional issue that you should consider is what happens when an attempt is made to set a non-object property to a nil value. In this case, the receiver sends itself a setNilValueForKey: message. The default implementation of setNilValueForKey: raises an NSInvalidArgumentException. Your application can override this method to substitute a default value or a marker value, and then invoke setValue:forKey: with the new value.

