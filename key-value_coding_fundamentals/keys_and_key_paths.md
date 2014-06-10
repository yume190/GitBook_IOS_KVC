# Keys and Key Paths
---

A key is a string that identifies a specific property of an object. Typically, a key corresponds to the name of an accessor method or instance variable in the receiving object. Keys must use ASCII encoding, begin with a lowercase letter, and may not contain whitespace.

Some example keys would be payee, openingBalance, transactions and amount.

A key path is a string of dot separated keys that is used to specify a sequence of object properties to traverse. The property of the first key in the sequence is relative to the receiver, and each subsequent key is evaluated relative to the value of the previous property.

For example, the key path address.street would get the value of the address property from the receiving object, and then determine the street property relative to the address object.

