# Key-Value Coding Accessor Methods
---

In order for key-value coding to locate the accessor methods to use for invocations of valueForKey:, setValue:forKey:, mutableArrayValueForKey:, and mutableSetValueForKey:, you need to implement the key-value coding accessor methods.

為了讓KVC去定位存取方法並調用`valueForKey:`, `setValue:forKey:`, `mutableArrayValueForKey:`, and `mutableSetValueForKey:`，你必須去實現KVC的存取方法

> Note: The accessor patterns in this section are written in the form `-set<Key>:` or `-<key>`. The `<key>` text is a placeholder for the name of your property. Your implementation of the corresponding method should substitute the property name for `<Key>` or `<key>` respecting the case specified by key. For example, for the property name, `-set<Key>:` would expand to `-setName:`, `-<key>` would simply be -name.
