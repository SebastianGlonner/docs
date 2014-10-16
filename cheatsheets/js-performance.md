# Summary of these sources
> http://www.smashingmagazine.com/2012/11/05/writing-fast-memory-efficient-javascript/

#  General
- Avoid using “delete” (performance loss due to structural changes of internal "hidden classes")
- Favour scoping over nullifying to garbage collect objects
- Take care of always clear timeouts and intervals

# Classes
- Std objects are much faster than constructor functions, use std. Objects if you dont need a constructor and no state, or want singleton anyway

# DOM
- Use "document.createDocumentFragment"
- Use event delegation (one event handler on the table instead of several on each cell

# Arrays VS Objects
- Integer-indexed elements, regardless of whether they’re stored in an array or an object, are much faster to iterate over than object properties
- When you need vectors, consider don’t define a class with properties x, y, z, but use an array instead.

# Objects
- Specially for “hot” objects, keep field count low and property chain short!
- Fast object cloning means, copy each property by hand explicit instead of “for ( … in … )” in a custom clone/constructor function

# Arrays
- Dont ever delete array items (might trigger Dictionary mode)
- Dont mix types of array items
- Avoid holes in an array (dont do: arr[x] = foo; // with x > arr.length)

# Memory
- dispatch event listener!
