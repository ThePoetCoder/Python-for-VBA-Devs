# Whitespace

I would argue that whitespace is very important in both Python and VBA for the *developer* to be able to read the code, but only in Python is the whitespace also important for the *computer* to be able to run the code. If you have gotten into a bad habit of neglecting to indent your code when the scope changes, then the way Python handles whitespace will come as quite a shock at first.

In the simplest terms possible, *almost* every time you write a colon `:` in Python, the lines below that need to be indented consistently until you wish to leave the scope of whatever you're working on.

Places you'll see colons used in Python include:
* Class Declarations
* Function Declarations
* if / elif / else statements
* Loops
* As a Slice operator

The note about indentation holds true in all of these places except for the final one when used as a Slice operator.

So, when writing an `if` statement in Python, you end the first line of that statement with a colon, and Python runs every line below it (that is indented consistently) if the statement evaluates to `True`. Here's an example:

```python
>>> if 1 == 1:
>>> ... print(1)
>>> ... print(2)
>>> ... print(3)
>>> ...
1
2
3
```
