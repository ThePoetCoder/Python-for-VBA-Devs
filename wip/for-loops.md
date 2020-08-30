---
created: 2020-08-30T17:29:12-05:00
modified: 2020-08-30T18:07:57-05:00
---

# for-loops

# For Loops in Python

VBA makes a distinction between a "for loop" and a "for each loop", but Python makes no such distinction. In fact, *every* "for loop" in Python is a "for each loop" as you know it. Let's go over some examples:

### For Loop in VBA
```vba
Dim i as Long

For i = 1 To 3
    Debug.Print i
Next

' outputs
1
2
3
```
This is very standard iteration over a few numbers. Note that we mark the upper and lower boundaries (1 and 3 respectively in the example) and both are included in the iteration and therefore printed to the Immediate Window. Now let's see the analogous functionality in Python:

### For Loop in Python
```python
>>> for i in range(1, 4):
>>> ... print(i)
>>> ...
1
2
3
```
Please note that not every for loop in Python requires the use of the `range` function displayed here, but that this is the most analogous code I could write to the above VBA.

Now let's look at the similarities and differences between an express "For Each loop" in VBA with its equivalent "for loop" in Python.

### For Each Loop in VBA
```vba
Dim ws as Worksheet

For Each ws in ActiveWorkbook.Sheets
    Debug.Print ws.Name
Next ws

' in a Workbook with 
' 3 default Worksheets
' this outputs
Sheet1
Sheet2
Sheet3
```
```python

```