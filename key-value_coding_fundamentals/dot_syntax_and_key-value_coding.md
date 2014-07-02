# Dot Syntax and Key-Value Coding
---

Objective-C’s dot syntax and key-value coding are orthogonal technologies. You can use key-value coding whether or not you use the dot syntax, and you can use the dot syntax whether or not you use KVC. Both, though, make use of a “dot syntax.” In the case of key-value coding, the syntax is used to delimit elements in a key path. Remember that when you access a property using the dot syntax, you invoke the receiver’s standard accessor methods.

ObjC的`.`語法和KVC是正交技術。你能使用KVC不論是否使用`.`語法，或者是你使用`.`語不論是否使用KVC。在KVC的例子中，這個語法用於`key paht`的分隔符號。記住！當你用`.`語法去存取property，相當於你去調用接收者的存取方法。

You can use key-value coding methods to access a property, for example, given a class defined as follows:

    @interface MyClass
    @property NSString *stringProperty;
    @property NSInteger integerProperty;
    @property MyClass *linkedInstance;
    @end

you could access the properties in an instance using KVC:

    MyClass *myInstance = [[MyClass alloc] init];
    NSString *string = [myInstance valueForKey:@"stringProperty"];
    [myInstance setValue:@2 forKey:@"integerProperty"];

To illustrate the difference between the properties dot syntax and KVC key paths, consider the following.

    MyClass *anotherInstance = [[MyClass alloc] init];
    myInstance.linkedInstance = anotherInstance;
    myInstance.linkedInstance.integerProperty = 2;

This has the same result as:

    MyClass *anotherInstance = [[MyClass alloc] init];
    myInstance.linkedInstance = anotherInstance;
    [myInstance setValue:@2 forKeyPath:@"linkedInstance.integerProperty"];
