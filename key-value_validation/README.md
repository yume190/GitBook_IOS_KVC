# Key-Value Validation
---

Key-value coding provides a consistent API for validating a property value. The validation infrastructure provides a class the opportunity to accept a value, provide an alternate value, or deny the new value for a property and give a reason for the error.

Validation Method Naming Convention

Just as there are conventions for naming accessor methods, there is a convention for naming a property’s validation method. A validation method has the format validate<Key>:error:. The example in Listing 1 shows the validation method declaration for the property name.

Listing 1  Validation method declaration for the property name
-(BOOL)validateName:(id *)ioValue error:(NSError * __autoreleasing *)outError {
    // Implementation specific code.
    return ...;
}
Implementing a Validation Method

Validation methods are passed two parameters by reference: the value object to validate and the NSError used to return error information.

There are three possible outcomes from a validation method:

The object value is valid, so YES is returned without altering the value object or the error.
The object value is not valid and a valid value cannot be created and returned. In this case NO is returned after setting the error parameter to an NSError object that indicates the reason validation failed.
A new object value that is valid is created and returned. In this case YES is returned after setting the value parameter to the newly created, valid value. The error is returned unaltered. You must return a new object, rather than just modifying the passed ioValue, even if it is mutable.
This variant is typically discouraged because it can be difficult to ensure values are propagated consistently.

The example in Listing 2 implements a validation method for a name property that ensures that the value object is a string and that the name is capitalized correctly.

Listing 2  Validation method for the name property
-(BOOL)validateName:(id *)ioValue error:(NSError * __autoreleasing *)outError{

    // The name must not be nil, and must be at least two characters long.
    if ((*ioValue == nil) || ([(NSString *)*ioValue length] < 2)) {
        if (outError != NULL) {
            NSString *errorString = NSLocalizedString(
                    @"A Person's name must be at least two characters long",
                    @"validation: Person, too short name error");
            NSDictionary *userInfoDict = @{ NSLocalizedDescriptionKey : errorString };
            *outError = [[NSError alloc] initWithDomain:PERSON_ERROR_DOMAIN
                                                    code:PERSON_INVALID_NAME_CODE
                                                userInfo:userInfoDict];
        }
        return NO;
    }
    return YES;
}
Important: A validation method that returns NO must first check whether the outError parameter is NULL; if the outError parameter is not NULL, the method should set the outError parameter to a valid NSError object.
Invoking Validation Methods

You can call validation methods directly, or by invoking validateValue:forKey:error: and specifying the key. The default implementation of validateValue:forKey:error: searches the class of the receiver for a validation method whose name matches the pattern validate<Key>:error:. If such a method is found, it is invoked and the result is returned. If no such method is found, validateValue:forKey:error: returns YES, validating the value.

Warning: An implementation of -set<Key>: for a property should never call the validation methods.
Automatic Validation

In general, key-value coding does not perform validation automatically—it is your application’s responsibility to invoke the validation methods.

Some technologies do perform validation automatically in some circumstances: Core Data automatically performs validation when the managed object context is saved; in OS X, Cocoa bindings allow you to specify that validation should occur automatically (see Cocoa Bindings Programming Topics for more information).

Validation of Scalar Values

Validation methods expect the value parameter to be an object, and as a result values for non-object properties are wrapped in an NSValue or NSNumber object as discussed in “Scalar and Structure Support.” The example in Listing 3 demonstrates a validation method for the scalar property age.

Listing 3  Validation method for a scalar property
-(BOOL)validateAge:(id *)ioValue error:(NSError * __autoreleasing *)outError {

    if (*ioValue == nil) {
        // Trap this in setNilValueForKey.
        // An alternative might be to create new NSNumber with value 0 here.
        return YES;
    }
    if ([*ioValue floatValue] <= 0.0) {
        if (outError != NULL) {
            NSString *errorString = NSLocalizedStringFromTable(
                @"Age must be greater than zero", @"Person",
                @"validation: zero age error");
            NSDictionary *userInfoDict = @{ NSLocalizedDescriptionKey : errorString };
            NSError *error = [[NSError alloc] initWithDomain:PERSON_ERROR_DOMAIN
                code:PERSON_INVALID_AGE_CODE
                userInfo:userInfoDict];
            *outError = error;
        }
        return NO;
    }
    else {
        return YES;
    }
    // ...
