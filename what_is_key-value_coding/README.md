# What Is Key-Value Coding?
---

Key-value coding is a mechanism for accessing an object’s properties indirectly, using strings to identify properties, rather than through invocation of an accessor method or accessing them directly through instance variables. In essence, key-value coding defines the patterns and method signatures that your application’s accessor methods implement.

KVC是一種間接存取物件屬性的機制，使用字串來辨別屬性，而不是透過調用存取方法或者直接存取實體變數，從本質上來說，KVC定義了模式和方法signatures你的應用程式的存取方法實現。

Accessor methods, as the name suggests, provide access to your application’s data model’s property values. There are two basic forms of accessor—get accessors and set accessors. Get accessors, also referred to as getters, return the values of a property. Set accessors, also referred to as setters, set the value of a property. There are getter and setter variants for dealing with both object attributes and to-many relationships.

存取方法，顧名思義，它提供了存取你的應用程式資料模型的屬性值，accessor有著2種的基礎形式get accessors 和 set accessors，get accessors被稱為getters，它會回傳屬性的值， set accessors也被稱為setters，它能設定屬性的值，There are getter and setter variants for dealing with both object attributes and to-many relationships.

Implementing key-value coding compliant accessors in your application is an important design principle. Accessors help to enforce proper data encapsulation and facilitate integration with other technologies such as key-value observing, Core Data, Cocoa bindings, and scriptability. Key-value coding methods can, in many cases, also be utilized to simplify your application’s code.

在你的應用程式實現KVC兼容存取子是一項非常重要的設計準則，存取子能夠幫助你執行正確的資料封裝以及便利的與其他技術整合，如KVO, Core Data, Cocoa bindings, scriptability.KVC方法在許多方面可以簡化你的應用程式Code
The essential methods for key-value coding are declared in the NSKeyValueCoding Objective-C informal protocol and default implementations are provided by NSObject.
KVC重要的方法定義在NSKeyValueCoding(Objective-c非正式的protocol)且NSObject預設已經實現。

Key-value coding supports properties with object values, as well as the scalar types and structs. Non-object parameters and return types are detected and automatically wrapped, and unwrapped, as described in “Scalar and Structure Support.”

