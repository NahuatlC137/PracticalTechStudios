---
---

Wooh! Existence. Simple enough for a simple post.

While working with data in Excel, often, the question "Does this data exist within another data set?" comes up. Below, I've outlined a couple of methods to accomplish this task.

### VLOOKUP or MATCH
My go-to method was *`=VLOOKUP(cell,single_column,1,0)`*. If the value exists, it simply returns itself, else #N/A, which means that the value doesn't exist.

![VLOOKUP](/assets/Exists_Using_VLOOKUP.PNG)

Similarly, the *`=MATCH(cell,single_column,0)`* method will yield the same outcome but instead of returning itself, it returns the first row number of the value you're after.

![MATCH](/assets/Exists_Using_MATCH.PNG)

### COUNTIF

[EXCELJET](https://exceljet.net/formula/value-exists-in-a-range "Visit EXCELJET") uses `=COUNTIF(range, cell) > 0`. This method counts the number of times a value exists within a given range. That's an added benefit as it doesn't limit the lookup to a single column.

![COUNTIF](/assets/Exists_Using_COUNTIF.PNG)

### UDF - User Defined Function Using VBA
