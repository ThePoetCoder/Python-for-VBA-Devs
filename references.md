# References

If you've spent any time at all with Python, you'll know that almost every Python script you see starts off with a number of `import` statements.

This allows Python scripts to wrap up and separately contain potentially huge amounts of code in scripts, modules, and packages outside of the currently running document, and be referenced anywhere a given script is `import`ed.

VBA has similar functionality built into it, mainly via the "References" window. For context, here is how you would reference the Scripting Runtime Module from VBA:

First, on the menu bar at the top, you would click on Tools > References... :

![VBA Ref 1](../master/images/vba_references_1.png)


Then you would find the correct module and check the box next to it:

![VBA Ref 2](../master/images/vba_references_2.png)


From there you would be able to declare a variable as an object found within the referenced library like so:

```vb
Dim FSO As Scripting.FileSystemObject
Set FSO = New Scripting.FileSystemObject

' use FSO object here

Set FSO = Nothing
```

This GUI approach to referencing code outside the current module is made possible because the VBE is so perfectly woven into the fabric of VBA. This is known as "early binding" as the `Dim` statement declares exactly what will be used. There is also a coded way of achieving the same effect, using the `CreateObject` method. This is known as "late binding" because the `Dim` statement only shows that the variable will be a generic Object type, and it later attached to the correct library and class via `CreateObject`. This "late binding" method does not require you to reference the library through the Menu bar, it will not give you Intellisense tips for the methods and properties available to that object, and should you be deploying your code to other people's computers, it will nit be as strict about which version of the library is being used. It looks like this:

```vb
Dim FSO As Object
Set FSO = CreateObject("Scripting.FileSystemObject")

' use FSO object here

Set FSO = Nothing
```
Python (in general, unless we're speaking about closures) is a lot more straightforward. As long as you have the file on your computer and reference it correctly, you will be able to use all the code inside as allowed.
