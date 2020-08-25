# Statement Delimiters

In both VBA and Python, the most common way to end a statement is by using a new line, but that is not the only way. In VBA you have the added option of using a colon to end a statement. For example, the bottom two bits of code would produce the same result:
```vb
' Way 1
Dim s as String
s = "Hi"

' Way 2
Dim s as String: s = "Hi"
```

So the colon `:` operator in VBA can be used to delimit statements of code that are being organized on a single line. Python has an identical mechanism with the semi-colon `;` operator instead. The below 2 bits of Python produce the same result as well:
```python
# Way 1
a = 3
print(a)

# Way 2
a = 3; print(a)

```

If for some reason you like keeping things together on the same line, you can still do that in Python. Just be aware, although it is syntactically possible to end every line of Python code with a semi-colon, it would be considered redundant and not very "Pythonic".
