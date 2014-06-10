# Key-Value Coding and Scripting
---

The scripting support in Cocoa is designed so that an application can easily implement scripting by accessing its model objects—the objects that encapsulate the application’s data. When the user executes an AppleScript command that targets your application, the goal is for that command to go directly to the application’s model objects to get the work done.

Scripting in OS X relies heavily on key-value coding to provide automatic support for executing AppleScript commands. In a scriptable application, a model object defines a set of keys that it supports. Each key represents a property of the model object. Some examples of scripting-related keys are words, font, documents, and color. The key-value coding API provides a generic and automatic way to query an object for the values of its keys and to set new values for those keys.

As you design the objects of your application, you should define the set of keys for your model objects and implement the corresponding accessor methods. Then when you define the script suites for your application, you can specify the keys that each scriptable class supports. If you support key-value coding, you will get a great deal of scripting support “for free.”

In AppleScript, object hierarchies define the structure of the model objects in an application. Most AppleScript commands specify one or more objects within your application by drilling down this object hierarchy from parent container to child element. You can define the relationships between properties available through key-value coding in class descriptions. See “Describing Property Relationships” for more details.

Cocoa’s scripting support takes advantage of key-value coding to get and set information in scriptable objects. The method in the Objective-C informal protocol `NSScriptKeyValueCoding` provides additional capabilities for working with key-value coding, including getting and setting key values by index in multi-value keys and coercing (or converting) a key-value to the appropriate data type
