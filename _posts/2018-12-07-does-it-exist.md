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

Because I was constantly checking if one dataset existed within another, I wrote a User Defined Function in VBA. Checkout the 18 lines of code below!

![COUNTIF](/assets/Exists_Using_UDF.PNG)

```vb
'Determines if a given value exists in a range.
'Defaults to True and False, with the option to return given true and false values.

Function EXISTSIN(ByVal CELL As Range, ByVal LOOK_IN_RANGE As Range, Optional ByVal TRUE_MATCH As String, Optional ByVal FALSE_MATCH As String)

'Declaring variables
Dim Exists As Boolean

    'using the match function from above nested within IsNumeric.
    'if the Match function returns a number, IsNumeric will set the Exists variable to True.
    'if the Match function doesn't return a number, IsNumeric will set the Exists variable to False.
    Exists = IsNumeric(Application.Match(CELL.Value, LOOK_IN_RANGE, 0))
    
    Select Case Exists
    
        '1. here, the function checks if variable Exists is True or False,
        '2. it checks whether or not the user is using the optional TRUE_MATCH or FALSE_MATCH strings
        'and define the output of EXISTSIN depending on 1 and 2.
        
        Case True
            If TRUE_MATCH = "" Then 'checking to see if TRUE_MATCH is blank
                EXISTSIN = Exists   'if TRUE_MATCH is blank, return the value of IsNumeric(Application.Match(CELL.Value, LOOK_IN_RANGE, 0))
            Else
                EXISTSIN = TRUE_MATCH 'if TRUE_MATCH isn't blank, then return what the user entered.
            End If
            
        Case False
        
            If FALSE_MATCH = "" Then 'checking to see if FALSE_MATCH is blank
                EXISTSIN = Exists    'if FALSE_MATCH is blank, return the value of IsNumeric(Application.Match(CELL.Value, LOOK_IN_RANGE, 0))
            Else
                EXISTSIN = FALSE_MATCH 'if FALSE_MATCH isn't blank, then return what the user entered.
            End If
    
    End Select

End Function
```

