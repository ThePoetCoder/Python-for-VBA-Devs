# Incrementing Variables

Python makes the process of incrementing a variable a little easier than VBA through the use of a specialized operator for that exact purpose. For reference, here is how you have to increment counter variables in VBA:

```vb
Dim count As Long

count = 5
count = count + 1

```

While code like this would work in Python, it is not very "Pythonic". Here is how this bit of code should be written in Python:

```python
count = 5
count += 1

```

Here the `+=` operator does the work of incrementing the variable for us. This operator is found in a number of other languages and is fairly well understood across the industry, so it is a shame that VBA does not have something similar, as it comes in handy quite often.

Similarly, you can use **any** of the standard 4 math operations to alter a variable:

```python
>>> count = 5
>>> count += 1
>>> count -= 2
>>> count *= 3
>>> count /= 4
>>> count
3.0
```

Notice how the result has a decimal place. This happens whenever you divide a number, regardless of whether a decimal went into the equation or not.
