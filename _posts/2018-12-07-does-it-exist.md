---
---

Wooh! Existence. Simple enough for a simple post.

While working with data in Excel, often, the question "Does this data exist within another data set?" comes up. Below, I've outlined a couple of methods to accomplish this task.

# Using a VLOOKUP or MATCH
My go-to was the `=VLOOKUP(cell,single_column,1,0)`. If the value exists, it simply returns the same value you're after, else #N/A, which means that the value doesn't exist.

![Exists](/assets/Exists_Using_VLOOKUP.PNG)

Similarly, `=MATCH(cell,single_column,0)` will yield the same outcome but instead of returning the lookup cell value, it returns the row number.

![Exists](/assets/Exists_Using_MATCH.PNG)
