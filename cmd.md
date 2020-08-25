# Running Python with VBA

When you want to run a Python file from Excel/VBA, the basic idea I've used successfully in the past (on Windows machines) is to write some VBA that calls a shell/command line interpreter and tells it both (1) where to find your Python file and (2) how to run it. There is, of course, 3rd party software available that can connect VBA & Python, but if you're looking for a native solution, this is a pretty good method.

In an effort to simplify the process of calling the command line, instead of simply telling you which VBA functions are capable of doing that and telling you the pros and cons of using each, I wrote out a function that tries to integrate calling the command line into VBA as seamlessly as possible, and a number of wrapper functions around this to make calling Python  and returning values back from it ridiculously easy. Here's the code:

* [VBA: Main 'cmd' function](../code/cmd_main)
* [VBA: Python Wrapper](../code/run_py)

Step by step, here's what you're going to do with the above code:
### Save the Code in an Add-in
1. Open a new/blank Excel workbook
2. Begin the process of saving the workbook and write in a title such as 'Command Line'
3. [Save as type ".xlam"](../images/addin.png)
4. Go to the Developer Tab
5. Click on "Excel Add-ins" (or just "Add-ins" on older versions of Excel)
6. Put a check next to whatever you titled your workbook
7. Hit "Ok"
8. Open the VBE
9. Find your workbook in the 'Project Explorer' of the VBE (CTRL + R if not visible)
10. [Right click the workbook and edit the properties](../images/vbaprop.png) to change the name to something recognizable, such as "CommandLine"
10. Insert 2 modules into your add-in, one for each of the links above
11. Copy/paste the code inside the links into the modules
12. Save the Add-in from the toolbar at the top of the VBE

### Use the Code Anywhere
Now you are ready to use this code anywhere in Excel! So let's say you start a new workbook and wish to be able to call Python from it. First you will [reference the CommandLine Add-in](../images/vba_references_1.png) (which is why it was helpful to rename the VBAProject to something more recognizable [by the time you get to the references form](../images/vba_references_2.png), and then you can freely call Python files directly from the new workbook.

Let's say you wish to simply run a Python file, no arguments passed, no return values coming back, simply run the code in a .py file. With the steps above followed, you can now write code like this:
```vb
Sub simple_example()
    straight_python_file_run "C:\Full\Path\To\File.py"
End Sub
```

Or if you need to pass an argument, like the value of the currently selected cell for example, you can do something like this:
```vb
Sub with_arugments()
    Dim argument_string As String
    argument_string = "-selection=" & Selection.Value
    
    straight_python_file_run "C:\Full\Path\To\File.py", argument_string
End Sub
```

When passing arguments, you will obviously need to account for those arguments being passed *into* Python as well, in which case the current best practice is to use the [argparse](https://docs.python.org/3/library/argparse.html) library. So in the above example, you would need to have some code that looks like this included in your Python file:
```py
arg_parser.add_argument("-selection")
```

As far as returning values back from Python into VBA/Excel, I have tried to make this as trivial as possible. Essentially, every time you call the `print()` function in Python, you have the opportunity to return what was printed to Excel/VBA using code like this on the VBA side:

```vb
Sub return_printed_values()
    Dim what_was_printed As String
    what_was_printed = python_udf("C:\Full\Path\To\File.py")
    
    'Do whatever you want with the value now
End Sub
```

So, in the example above, if "C:\Full\Path\To\File.py" was a Python file that had a single line of code that said:
```py
print("Hello, World!")
```

then this would pass "Hello, World!" into the String variable `what_was_printed` when you called the `return_printed_values` subroutine from Excel/VBA.

### Examples
Below I have 2 fully-fledged and working examples of this code in practice, on both the VBA & Python sides, showing how you can use VBA to make a UDF that calls Python with arguments passed into the VBA function and returns the values back from Python as the result of the UDF. This is pretty powerful stuff once you realize that all of Python is now available to you in Excel!

* [Example 1: String Slice](../code/slice) - Adding a UDF to Excel that can slice strings in the Python way, with a worksheet formula like `=py_slice("Testing", 2, 5)` being equivalent to the Python code `"Testing"[2:5]`.

* [Example 2: Fuzzy Percent](../code/fuzzy) - Return a % of how similar 2 strings are to one another in Excel, with a worksheet formula such as `=fuzzy_comp("The Poet Coder", "Coding is Poetry")`
