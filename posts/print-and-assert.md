# Print & Assert

Python & VBA are very similar in the way they print & assert information during runtime. For reference, here is how it looks in VBA:

```vb
Sub print_and_assert()
    Dim message as String
    
    message = "Hello, World!"
    Debug.Print message
    Debug.Assert message = "Hi, World"
    
End Sub
```

and as you can see below, this is almost identical to the syntax you would use in Python to achieve the same functionality:

```python
def print_and_assert():
    message = "Hello, World!"
    print(message)
    assert message == "Hi, World!"
```
So this is wonderfully easy to switch over to; you basically just drop the `Debug.`, and be sure to remember that Python uses `==` to test for equality.

---

There is a slightly bigger difference in the way the assert keywords work however. In VBA, the program will run until it hits a false assert statement and stop running, allowing you to edit the code during runtime and continue if desired; Python has no such functionality. In Python, when you hit a false assert statement, the program will fail with an AssertionError, and simply let you know on which line the failed assertion occurs.

Here's an example of  failed assertion in VBA:

![VBA Assert Fail](../images/vba_assert_fail.png)


And here's an example of a failed assertion in Python:

![Py Assert Fail](../images/py_assert_fail.png)
