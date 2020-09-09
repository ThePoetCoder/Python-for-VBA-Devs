# Whitespace

I would argue that whitespace is very important in both Python and VBA for the *developer* to be able to read the code, but only in Python is the whitespace also important for the *computer* to be able to run the code. If you have gotten into a bad habit of neglecting to indent your code when the scope changes, then the way Python handles whitespace will come as quite a shock at first.

In the simplest terms possible, *almost* every time you write a colon `:` in Python, the lines below that need to be indented consistently until you wish to leave the scope of whatever you're working on.

Places you'll see colons used in Python include:
* Class Declarations
* Function Declarations
* if / elif / else statements
* Loops
* As a Slice operator

The note about indentation holds true in all of these places except for the final one when colons are used as a Slice operator.

For example, when writing an `if` statement in Python, you end the first line of that statement with a colon, and Python runs every line below it (that is indented consistently) if the statement evaluates to `True`. Here's an example:

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

Or take a simple function declaration:
```python
# correct
def my_function():
    return True

# incorrect
def my_function():
return True
```
Without the indentation shown in the correct example above, the code would fail with a very appropriately name "IndentationError", and say "IndentationError: expected an indented block" in the error message. Python does not care whether you use a single space or 1,000 (I have not tested higher than that, nor should you come anywhere close to this) to indent your lines, as long as they are all *consistent* with each other. The standard is 4 spaces, which can be typed into PyCharm with a single click of the Tab button (or obviously with 4 clicks of the spacebar as well). So if the first line of indentation you use 4 spaces and the next line you use 5, you will get the error "IndentationError: unexpected indent".

It follows then if you have scopes within scopes that you will need to continue indenting in this same pattern. Consider the following example:

```python
def is_it_1(var):
    if var == 1:
        return True
    return False
```
Here we define a function called `is_it_1` that takes a single argument labeled `var`. If `var == 1` then the function returns the boolean value `True`, otherwise that doubly-indented line of the code is skipped over and the function returns `False` instead. Note that the line `if var == 1:` and `return False` are both indented at the same level / number of spaces, indicating they are both within exactly the same scope. You could rewrite the function like this for the **exact** same results:
```python
def is_it_1(var):
    if var == 1:
        return True
    else:
        return False
```
If you find that your code is beginning to look like a staircase (of scopes inside scopes inside scopes...) then it is definitely time to reconsider the problem and think about how you could break it down into smaller pieces. Just how many levels / indents in you should start to worry about this depends a lot on which scopes you're using (I wouldn't count Class or Function declarations against your total levels) and the overall simplicity of your program. Different people have different tolerances for this sort of thing, and when in doubt, try to write it so that it's easy for you to explain what's going on inside each scope and the potential and boundaries for that scope.
