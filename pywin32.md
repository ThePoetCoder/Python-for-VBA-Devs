# The pywin32 Library

Want to write executable Python code with the syntax of VBA? Look no further than [the pywin32 library!](https://github.com/mhammond/pywin32)

Written by the great [Mark Hammond](https://www.reddit.com/r/Python/comments/402ccx/help_me_appreciate_mark_hammond/), it will provide you a clean and simple way to write code that interacts with Windows objects, exactly like it should, right out of the box.

Let's say you wanted to do the following:
1. Open up a new Excel Workbook
2. Write some values into cells
3. Color some cells
4. Delete Column A
5. Change the worksheet's name
6. Open the workbook up to view it

With pywin32, that process would look like this:
```py
import win32com.client as win32

# Excel Constants
xlToLeft = -4159
xlMaximized = -4137

# Get an instance of an Excel Application object
application = win32.Dispatch("Excel.Application")
for add_in in application.AddIns:
    if add_in.Installed:
        add_in.Installed = False
        add_in.Installed = True
application.ScreenUpdating = False

# 1. Open up a new Excel Workbook
wb = application.Workbooks.Add()
xl_window = wb.Windows(1)
xl_window.Visible = False
ws = wb.ActiveSheet

# 2. Write some values into cells
ws.Range("B1").Value = "Hello"
ws.Range("B2").Value = 99
ws.Range("C1").Value = 1 / 3
ws.Range("C2").Value = True

# 3. Color some cells
ws.Range("B1:B2").Interior.Color = 255
ws.Range("C1:C2").Interior.Color = 5296274

# 4. Delete Column A
ws.Columns("A:A").Delete(Shift=xlToLeft)

# 5. Change the worksheet's name
ws.Name = "New Name"

# 6. Open the workbook up to view it
xl_window.Visible = True
xl_window.WindowState = xlMaximized
application.ScreenUpdating = True

```
That probably looks like a pretty familiar syntax to you! The biggest differences are likely the beginning and end of that bit of code, being the code prior to step #1 and the code in step #6. So let's go step by step through this to make sure you understand why each piece is needed.

```py
import win32com.client as win32
```
This is a standard `import` statement for python, bringing in the `win32com.client` library, to be used by the name `win32` from then on.

```py
# Excel Constants
xlToLeft = -4159
xlMaximized = -4137
```
This is setting up the ability to call Excel constants in the normal way later on in the script. Normally, when you want to find out the specific value for any Excel constant, you'll need to open up the VBE, go into your Object Explorer (press F2), and search for the constant you want to use. The value should be able to be seen upon finding & clicking on the constant, and you can actually copy & paste the constant and the value out of the VBE and directly into your python script, as seen in [this picture.](../images/object_explorer) 

I actually have created an easier way to use/look up Excel constants in particular, and you can find that [here] or [here].
