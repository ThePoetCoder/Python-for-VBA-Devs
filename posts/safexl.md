# The safexl Library

Want to write executable Python code with the syntax of VBA? Look no further than [safexl](https://github.com/ThePoetCoder/safexl)!

safexl serves as wrapper around [the pywin32 library](https://github.com/mhammond/pywin32) written by the great [Mark Hammond](https://www.reddit.com/r/Python/comments/402ccx/help_me_appreciate_mark_hammond/). This provides you a clean and simple way to write code that interacts with Windows objects, exactly like it should, right out of the box.

Installing safexl is as easy as opening up a command prompt and typing in `pip install safexl` (please note this is a Windows-only library).

Let's say you wanted to do the following:
1. Open up a new Excel Workbook
2. Write some values into cells
3. Color some cells
4. Delete Column A
5. Change the worksheet's name
6. Open the workbook up to view it

With safexl, that process would look like this:
```python
import safexl

with safexl.application(kill_after=False, maximize=True, include_addins=True) as app:
    # 1. Open up a new Excel Workbook
    wb = app.Workbooks.Add()
    ws = wb.ActiveSheet

    # 2. Write some values into cells
    ws.Range("B1").Value = "Hello"
    ws.Range("B2").Value = 99
    ws.Range("C1").Value = 1 / 3
    ws.Range("C2").Value = True

    # 3. Color some cells
    ws.Range("B1").Interior.Color = safexl.colors.rgbRed  # colors are included
    
    # 4. Delete Column A
    ws.Columns("A").Delete(Shift=safexl.xl_constants.xlToLeft)  # constants are included

    # 5. Change the worksheet's name
    ws.Name = "New Name"

# 6. Open the workbook up to view it (occurs at the end of this `with` block when `kill_after=False` above)

```
That probably looks like a pretty familiar syntax to you! The biggest differences are at the beginning of that bit of code, being the 2 lines of code prior to step #1. So let's look at those first 2 lines to make sure you understand why each is needed.

```python
import safexl
```
This is a standard `import` statement for python, bringing in the `safexl` library. Importing a library is similar to how the VBE allows you to [reference](../master/references.md) other libraries. 

```python
with safexl.application(kill_after=False, maximize=True, include_addins=True) as app:
```

That's a lot going on in one line. The safexl library includes a function called `application` that we are calling on here by using a `with` block. Imagine a `with` block as being a way to tell Python to clean up after itself. Everything you indent beneath this line of code is contained by the context of the `application` function, and as soon as you un-indent a single line of code the function will remove your access to the application object as well as close down this instance of Excel. This happens instead of you having to write out code like `application.Quit()` or anything like that and occurs even if you encounter an error inside your `with` block.

Being passed to the application function are 3 parameters titled `kill_after`, `maximize`, and `include_addins`. 
* `kill_after` indicates your desire to close the application object after you exit the `with` block. In this case, since we wish to open Excel and view our work, we set it to `False`.
* `maximize` indicates whether you would like the Excel window to be maximized once you leave the `with` block
* `include_addins` indicates whether you would like to include addins you have set up in Excel in *this* instance of Excel. By default Excel will not load addins when it is instantiated from code (neither VBA or Python). This parameter goes the extra mile to turn those addins you have loaded in Excel on for this instance as well.

Finally we see `as app:` which is simply the variable we are storing the application object to for the duration of the `with` block. In VBA this is analogous to the way `Application` is able to be wielded. We could write any python-valid variable name there instead of `app`. So when we are finally inside the `with` block you can see the first line references our variable name to create a workbook with the line `wb = app.Workbooks.Add()`. For more info on `with` blocks, check out [this article](https://realpython.com/python-keywords/#structure-keywords-def-class-with-as-pass-lambda) from Real Python.

So if you're considering picking up Python as a language to keep in your toolbelt, using it alongside safexl is a great way to ease the transition.
