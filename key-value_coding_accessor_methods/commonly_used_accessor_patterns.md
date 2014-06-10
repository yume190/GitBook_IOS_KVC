# Commonly Used Accessor Patterns
---

The format for an accessor method that returns a property is -<key>. The -<key> method returns an object, scalar, or a data structure. The alternate naming form -is<Key> is supported for Boolean properties.

The example in Listing 1 shows the method declaration for the hidden property using the typical convention, and Listing 2 shows the alternate format.

__Listing 1__  Accessor naming variations for a hidden property key
    - (BOOL)hidden {
       // Implementation specific code.
       return ...;
    }
    Listing 2  Alternate form accessor for a hidden property key
    - (BOOL)isHidden {
       // Implementation specific code.
       return ...;
    }

In order for an attribute or to-one relationship property to support setValue:forKey:, an accessor in the form set<Key>: must be implemented. Listing 3 shows an example accessor method for the hidden property key.

Listing 3  Accessor naming convention to support a hidden property key

    - (void)setHidden:(BOOL)flag {
       // Implementation specific code.
       return;
    }

If the attribute is a non-object type, you must also implement a suitable means of representing a nil value. The key-value coding method setNilValueForKey: method is called when you attempt to set an attribute to nil. This provides the opportunity to provide appropriate default values for your application, or handle keys that don’t have corresponding accessors in the class.

The following example sets the hidden attribute to YES when an attempt is made to set it to nil. It creates an NSNumber instance containing the Boolean value and then uses setValue:forKey: to set the new value. This maintains encapsulation of the model and ensures that any additional actions that should occur as a result of setting the value will actually occur. This is considered better practice than calling an accessor method or setting an instance variable directly.

    - (void)setNilValueForKey:(NSString *)theKey {

        if ([theKey isEqualToString:@"hidden"]) {
            [self setValue:@YES forKey:@"hidden"];
        }
        else {
            [super setNilValueForKey:theKey];
        }
    }
