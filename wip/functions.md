# Functions

In Python, functions are described as being "First Class Objects" which is definitely not the case in VBA. While you can obviously choose to ignore this capability in Python, the possibilities available because of it are extraordinary.

In practical terms having functions as First Class Objects means you can treat the name of a function (set up during its definition/declaration) the same as any other variable. Let's take the builtin Python function `sum` as an example:

```python
>>> print(sum)
<built-in function sum>
>>> print(sum([1, 2, 3]))
6
>>> my_variable = sum
>>> print(my_variable)
<built-in function sum>
>>> print(my_variable([1, 2, 3]))
6
```
Here I've displayed a few things to go over on this topic. 

The first line is an interesting one, especially coming from a VBA background; to call a function in Python you *must* use parentheses after it. VBA only [requires parentheses](https://docs.microsoft.com/en-us/office/vba/language/concepts/getting-started/using-parentheses-in-code) for subroutines and functions if you use the `Call` keyword ahead of the subroutine or wish to get a return value out of a function. In Python, leaving the parentheses off is an indication you wish to *reference the function itself* as opposed to call it / return an answer from it. So when I execute the line `print(sum)` in a REPL, the result is `<built-in function sum>` which indicates I have referenced the function without calling it. My next line displays the way to properly call the sum function, I have parentheses after the name sum, and am passing an iterable (in this instance a list) to the function, and it sums up the contents and returns the result 6 as the sum of the number 1, 2, and 3.

Then I do something else very odd coming from VBA, is I assign the function to another variable name, `my_variable`. After this line in the REPL executes there are now 2 function names with the ability to sum the contents of an iterable, both `sum` and `my_variable`. I prove this by going on to repeat the functionaility displayed by the sum function itself using `my_variable` instead.
