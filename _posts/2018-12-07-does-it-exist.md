---
---

Wooh! Existence. Simple enough.

While working with data in Excel, often, the question "Does this data exist within another data set?" comes up. Below, I've outlined a couple of methods to accomplish this task.

### VLOOKUP or MATCH
My go-to function was `=VLOOKUP(cell,single_column,1,0)`. If the value exists, it simply returns itself, else #N/A, which means that the value doesn't exist.

![VLOOKUP](/assets/Exists_Using_VLOOKUP.PNG)

Similarly, the function `=MATCH(cell,single_column,0)` will yield the same outcome but instead of returning itself, it returns the row number of the found value, else #N/A.

![MATCH](/assets/Exists_Using_MATCH.PNG)

### COUNTIF

[EXCELJET](https://exceljet.net/formula/value-exists-in-a-range "Visit EXCELJET") uses `=COUNTIF(range, cell) > 0`. This method counts the number of times a value exists within a given range. Using `COUNTIF` doesn't limit the lookup to a single column, meaning you can check across multiple columns.

![COUNTIF](/assets/Exists_Using_COUNTIF.PNG)

### UDF - User Defined Function Using VBA

Because I was constantly checking if one dataset existed within another, I wrote a User Defined Function.
