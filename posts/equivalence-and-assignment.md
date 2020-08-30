# Equivalence & Assignment

Python has the exact same syntax for assigning variables, but a slightly different syntax than VBA for testing equivalence . To put it simply:


| Type |   VBA  | Python |
|:-----|:-------|:-------|
|Assignment |  =   |  =|
|Equal      |  =   |  ==|
|Not Equal  |  <>   | !=|


In VBA, the `=` operator works for both assignment and equivalence testing. So something like this is valid VBA code:

```vb
a = 5
If a = 5 Then
    Debug.Print "It Worked"
End If

```

Using the `=` operator the same way in Python will cause a Error

```python
>>> a = 5
>>> if a = 5:
    File "<stdin>", line 1
        if a = 5:

SyntaxError: invalid syntax
```

Instead you have to use the `==` operator:
```python
>>> a = 5
>>> if a == 5:
...     print("It Worked")
...
It Worked
```
