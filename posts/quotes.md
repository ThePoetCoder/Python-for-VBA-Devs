# Quotes

The way VBA handles quotations as a language is, in a word, ridiculous. While Python handles string creation in general with much more ease, coming from a VBA background you will find that quotes in particular are much easier to deal with.

Stemming from the fact that a single quote signifies the beginning of a comment in VBA, it relies on varying numbers of double quotes if you wish to have quotes within quotes, like this:

```vb
Sub vba_double_quotes()
    Debug.Print 2, ""
    Debug.Print 4, """"
    Debug.Print 6, """"""
    Debug.Print 8, """"""""
    
End Sub

' Running this sub would print the following to the Immediate Window:
' 2
' 4    "
' 6    ""
' 8    """

```

This makes close to no sense. Granted, there's never going to be a reason you need to print three double quotes in a row, but I guarantee that if you did, using eight double quotes in your code is not the most intuitive way to go about it.
Printing a single double quote is pretty common however, and using four double quotes to achieve that just seems wrong. Sure you can just use `chr(39)` for single quotes and `chr(34)` for double quotes, and sometimes you have to with VBA, but there has to be a better way.

### Enter Python!

As with most things, Python makes working with strings and quotes within strings a breeze. Because it is not held back by using a single quote for other purposes, Python is able to begin strings with either single OR double quotes.
```py
a = "Double quotes can make strings"
b = 'Single quotes can too!'

```

And if you need quotes within quotes, just use the opposite of what you used on the outside, as in use double quotes within single quotes, or vice versa. The following Python code would print the same results as the VBA above:
```py
def python_double_quotes():
    print(2)
    print(4, '"')
    print(6, '""')
    print(8, '"""')

```

If you need to use single quotes within a string, just use double quotes on the outside:
```py
def python_single_quotes():
    print(2)
    print(4, "'")
    print(6, "''")
    print(8, "'''")
    
```

But what if you need to get really fancy and use single quotes inside double quotes inside single quotes? Python's got you covered there too, via use of the escape character (\\) in string building:
```py
>>> print('The bank teller said "I\'m sorry, I can\'t do that."')
The bank teller said "I'm sorry, I can't do that."

```

For reference, here is what it would take to build the above string in VBA:
```vb
Debug.Print "The bank teller said " & chr(34) & "I" & chr(39) & "m sorry, I can" & chr(39) & "t do that." & chr(34)

```

Which would you rather write out?
