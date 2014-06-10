# Terminology

---

In addition to overloading existing terms, key-value coding defines some unique terminology of its own.

In addition to overloading existing terms,KVC定義了一些它自己特有的術語

Key-value coding can be used to access three different types of object values: attributes, to-one relationships, and to-many relationships. The term property refers to any of these types of values.

KVC可用於存取三種不同的物件值：attributes, to-one relationships, and to-many relationships. The term property refers to any of these types of values.

An attribute is a property that is a simple value, such as a scalar, string, or Boolean value. Value objects such as NSNumber and other immutable types such as as NSColor are also considered attributes.

attribute是一個簡單值的property，舉例來說 存量，字串或者布林值。Value objects 例如NSNumber和其他不可變的類型如NSColor也被歸類與此。

A property that specifies a to-one relationship is an object that has properties of its own. These underlying properties can change without the object itself changing. For example, an NSView instance’s superview is a to-one relationship.

property也說明了一個物件自己擁有properties的一對一的關係。這些相關properties可以獨立改變。舉例來說，NSView的superview是一種一對一關係。

Finally, a property that specifies a to-many relationship consists of a collection of related objects. An instance of NSArray or NSSet is commonly used to hold such a collection. However, key-value coding allows you to use custom classes for collections and still access them as if they were an NSArray or NSSetby implementing the key-value coding accessors discussed in “Collection Accessor Patterns for To-Many Properties.”

最後，
