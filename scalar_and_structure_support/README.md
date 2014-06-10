# Scalar and Structure Support
---
Key-value coding provides support for scalar values and data structures by automatically wrapping and unwrapping NSNumber and NSValue instance values.

Representing Non-Object Values

The default implementations of valueForKey: and setValue:forKey: provide support for automatic object wrapping of the non-object data types, both scalars and structs.

Once valueForKey: has determined the specific accessor method or instance variable that is used to supply the value for the specified key, it examines the return type or the data type. If the value to be returned is not an object, an NSNumber or NSValue object is created for that value and returned in its place.

Similarly, setValue:forKey: determines the data type required by the appropriate accessor or instance variable for the specified key. If the data type is not an object, then the value is extracted from the passed object using the appropriate -<type>Value method.

Handling nil Values

An additional issue arises when setValue:forKey: is invoked with nil passed as the value for a non-object property. There is no generalized action that is appropriate. The receiver is sent a setNilValueForKey: message when nil is passed as the value for a non-object property. The default implementation of setNilValueForKey: raises an NSInvalidArgumentException exception. A subclass can override this method to provide the appropriate implementation specific behavior.

The example code in Listing 1 responds to an attempt to set a person’s age, a float value, to a nil value by instead setting the age to 0.

Note: For backward binary compatibility, unableToSetNilForKey: is invoked instead of setNilValueForKey: if the receiver’s class has overridden the NSObject implementation of unableToSetNilForKey:.
Listing 1  Example implementation of setNilValueForKey:
- (void)setNilValueForKey:(NSString *)theKey
{
    if ([theKey isEqualToString:@"age"]) {
        [self setValue:[NSNumber numberWithFloat:0.0] forKey:@"age"];
    } else
        [super setNilValueForKey:theKey];
}
Wrapping and Unwrapping Scalar Types

Table 1 lists the scalar types that are wrapped using NSNumber instances.

Table 1  Scalar types as wrapped in NSNumber objects
Data type
Creation method
Accessor method
BOOL
numberWithBool:
boolValue
char
numberWithChar:
charValue
double
numberWithDouble:
doubleValue
float
numberWithFloat:
floatValue
int
numberWithInt:
intValue
long
numberWithLong:
longValue
long long
numberWithLongLong:
longLongValue
short
numberWithShort:
shortValue
unsigned char
numberWithUnsignedChar:
unsignedChar
unsigned int
numberWithUnsignedInt:
unsignedInt
unsigned long
numberWithUnsignedLong:
unsignedLong
unsigned long long
numberWithUnsignedLongLong:
unsignedLongLong
unsigned short
numberWithUnsignedShort:
unsignedShort
Wrapping and Unwrapping Structs

Table 2 shows the creation and accessor methods use for wrapping the common NSPoint, NSRange, NSRect, and NSSize structs.

Table 2  Common struct types as wrapped using NSValue.
Data type
Creation method
Accessor method
NSPoint
valueWithPoint:
pointValue
NSRange
valueWithRange:
rangeValue
NSRect
valueWithRect: (OS X only).
rectValue
NSSize
valueWithSize:
sizeValue
Automatic wrapping and unwrapping is not confined to NSPoint, NSRange, NSRect, and NSSize—structure types (that is, types whose Objective-C type encoding strings start with {) can be wrapped in an NSValue object. For example, if you have a structure and class like this:

typedef struct {
    float x, y, z;
} ThreeFloats;

@interface MyClass
- (void)setThreeFloats:(ThreeFloats)threeFloats;
- (ThreeFloats)threeFloats;
@end
Sending an instance of MyClass the message valueForKey: with the parameter @"threeFloats" will invoke the MyClass method threeFloats and return the result wrapped in an NSValue. Likewise sending the instance of MyClass a setValue:forKey: message with an NSValue object wrapping a ThreeFloats struct will invoke setThreeFloats: and pass the result of sending the NSValue object a getValue: message.

Note: This mechanism doesn’t take reference counting or garbage collection into account, so take care when using with object-pointer-containing structure types.
