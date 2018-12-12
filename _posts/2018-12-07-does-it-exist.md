---
classes: wide
---

Wooh! Existence. Simple enough.

While working with data in Excel, often, we question "Does this data exist within another data set?". Below, I've outlined a couple of methods to accomplish this task.

##### VLOOKUP or MATCH
My go-to function was `=VLOOKUP(cell,single_column,1,0)`. If the value exists, it simply returns itself, else #N/A, which means that the value doesn't exist.

![VLOOKUP](/assets/Exists_Using_VLOOKUP.PNG)

[MATCH](https://docs.microsoft.com/en-us/office/vba/api/excel.worksheetfunction.match) will yield the same result, albeit, if the value exists, the function will return the row number of the found value.

##### COUNTIF

[EXCELJET](https://exceljet.net/formula/value-exists-in-a-range "Visit EXCELJET") uses `=COUNTIF(range, cell) > 0`. This method counts the number of times a value exists within a given range. `COUNTIF` has the added ability to check across multiple columns.

![COUNTIF](/assets/Exists_Using_COUNTIF.PNG)

##### UDF - User Defined Function Using VBA

Because I was constantly checking if one dataset existed within another, I wrote a User Defined Function in VBA. Checkout the 18 lines of code below! I've commented a good bit to help explain the code.

The idea is that TRUE or FALSE outputs won't always clearly explain what's going on in the data. Using the optional TRUE_MATCH or FALSE_MATCH string variables will help in that aspect.


```vb

Function EXISTSIN(ByVal CELL As Range, ByVal LOOK_IN_RANGE As Range, Optional ByVal TRUE_MATCH As String, Optional ByVal FALSE_MATCH As String)

'Declaring variables
Dim Exists As Boolean

    'using the CountIf function, EXISTSIN can look across multiple columns.
    'if CountIf is greater than 0, it sets the Exists variable to TRUE.
    'if CountIf is 0, it sets the Exists variable to FALSE.
    Exists = Application.CountIf(LOOK_IN_RANGE, CELL.Value) > 0
    
    Select Case Exists
    
        '1. here, the function checks if variable Exists is set to TRUE or FALSE,
        '2. it checks whether or not the user is using the optional TRUE_MATCH or FALSE_MATCH strings
        'and define the output of EXISTSIN depending on 1 and 2.

        Case True
            If TRUE_MATCH = "" Then'checking to see if TRUE_MATCH is blank
                EXISTSIN = Exists   'if TRUE_MATCH is blank, simply return TRUE
            Else
                EXISTSIN = TRUE_MATCH 'if TRUE_MATCH isn't blank, then return what the user entered.
            End If
            
        Case False
        
            If FALSE_MATCH = "" Then 'checking to see if FALSE_MATCH is blank
                EXISTSIN = Exists    'if FALSE_MATCH is blank, simply return FALSE
            Else
                EXISTSIN = FALSE_MATCH 'if FALSE_MATCH isn't blank, then return what the user entered.
            End If
    
    End Select

End Function
```
As an illustration, column E and F contain World Cup finalists up to 2014. In column H, there are 4 countries for which to find out if they have ever been a World Cup finalist.

Simply typing `=EXISTSIN(cell,range)` will yield standard TRUE and FALSE outputs. Alternatively, by entering a different TRUE or FALSE default, the analysis becomes clear to the reader.

`=EXISTSIN(cell, range, "Finalist", "Not a Finalist")` makes clear who was and who wasn't in a final match.

![COUNTIF](/assets/Exists_Using_UDF.PNG)