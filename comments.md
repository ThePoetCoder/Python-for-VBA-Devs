# Commenting Your Code

There is only a small difference commenting in VBA & commenting in Python
```vb
' a single quote is how you comment in VBA

```

```python
# a pound sign/hashtag is how you comment in Python

```

Comments are used in exactly the same way, in exactly the same places.

Python has the additional use of triple double-quotes to comment code. The most often place you'll see this is at the beginning of a function, class, or module.

And it looks like this:

```python
def add_two(a, b):
    """Add two numbers together
    a: number, either int or float
    b: number, either int or float
    
    returns: sum of the 2 inputs
    """
    
    return a + b

add_two(1, 2)
```

Technically though, the triple quote form of commenting is not so much a comment as it is creating a string that is never used again. Therefore, you are not able to create an inline comment using the triple quote:
```python
>>> a = 5
>>> a + 5 """inline comment will fail"""
SyntaxError: invalid syntax
```
