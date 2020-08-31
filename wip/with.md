# With Blocks

In VBA the whole point of a `With` block is to save you some typing and be able to reference things with only a period (.) but in Python `with` blocks are much more focused on automatic resources cleanup.

VBA's `With` keyword prevents you from needing to fully qualify your object each time it is referenced. Let's take the following bit of code for example:

```vba
With ActiveSheet.Range("A1")
    .Value = 1
    .Interior.Color = 255
End With
```

Here we can see that we reference `ActiveSheet.Range("A1")` multiple times inside the `With` block using only a period.

In Python