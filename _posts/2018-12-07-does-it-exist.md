---
---

Wooh! Existence. Simple enough for a simple post.

While working with data in Excel, often, the question "Does this data exist within another data set?" comes up. There are several methods of accomplishing this task.

My go-to was the =VLOOKUP(cell,single_column,1,0). If the value exists, it simply returns the same value you're after, else #N/A, which means that the value doesn't exist.

![Exists using VLOOKUP]:
(https://github.com/NahuatlC137/PracticalTechStudios/blob/master/assets/Exists_Using_VLOOKUP.PNG)
