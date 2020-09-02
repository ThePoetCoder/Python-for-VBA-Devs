# Functions

In Python, functions are described as being "First Class Objects" which is definitely not the case in VBA. While you can obviously choose not to make use of this capability in Python, the possibilities brought about because of it are nothing short of extraordinary.

In practical terms this means you can treat the name of a function the same as any other variable. Let's take the builtin Python function `sum` as an example:

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
Here I've displayed a few things to go over on this topic. The first line is an interesting one, especially coming from a VBA background; to call a function in Python you *must* use parentheses after it. [VBA only requires parentheses](https://docs.microsoft.com/en-us/office/vba/language/concepts/getting-started/using-parentheses-in-code) for subroutines and functions if you use the `Call` keyword ahead of the subroutine or wish to get a return value out of a function. So when I execute the line `print(sum)` what it printed to the command line REPL is