# Using Key-Value Coding to Simplify Your Code
---

You can use key-value coding methods in your own code to generalize implementations. For example, in OS X NSTableView and NSOutlineView objects both associate an identifier string with each of their columns. By making this identifier the same as the key for the property you wish to display, you can significantly simplify your code.

Listing 1 shows an implementation of an NSTableView delegate method without using key-value coding. Listing 2 shows an implementation that takes advantage of key-value coding to return the appropriate value using the column identifier as the key.

__Listing 1__  Implementation of data-source method without key-value coding
    - (id)tableView:(NSTableView *)tableview
          objectValueForTableColumn:(id)column row:(NSInteger)row {

        ChildObject *child = [childrenArray objectAtIndex:row];
        if ([[column identifier] isEqualToString:@"name"]) {
            return [child name];
        }
        if ([[column identifier] isEqualToString:@"age"]) {
            return [child age];
        }
        if ([[column identifier] isEqualToString:@"favoriteColor"]) {
            return [child favoriteColor];
        }
        // And so on.
    }

__Listing 2__  Implementation of data-source method with key-value coding

    - (id)tableView:(NSTableView *)tableview
          objectValueForTableColumn:(id)column row:(NSInteger)row {

        ChildObject *child = [childrenArray objectAtIndex:row];
        return [child valueForKey:[column identifier]];
    }
