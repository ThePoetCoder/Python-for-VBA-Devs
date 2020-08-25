# PyCharm's Keymap

PyCharm has a number of keyboard shortcuts built in to help you navigate the IDE without the use of a mouse. Some of my favorites and most often used are:

Command | Action
--- | ---
CTRL + D | Duplicate line above, same as an Excel Worksheet
Alt + Shift + Up Arrow | Move current line up to line above
Alt + Shift + Down Arrow | Move current line down to line below
CTRL + Shift + 10 | Run code in active tab
CTRL + Shift + 9 | Debug code in active tab
CTRL + / | Comment/Uncomment the selected line(s) of code
Alt + F8 | Evaluate Expression (during debugging mode)
F8 | Execute current line only (during debugging mode)

But here's the thing; I wanted to change one of the Keyboard Shortcuts to be more like I remembered from the VBE. Specifically, there is a command they call "Step Into My Code" that you can use during debugging mode that acts identically to the way F7 works in the VBE during debugging mode, as in if the current line contains a function or method call (of code you wrote, not 3rd party library code) it will step into that code and continue to allow you to go line by line in the function or method. And here's how I accomplished that:

Go into `File > Settings > Keymap` and you will find a subcutaneous tree-mapping of all actions that are available in the IDE. The one we are looking for is found under `Main Menu > Run > Force Step Into` (don't ask me why they call it "Step Into my Code" within the IDE and "Force Step Into" in the keymap, but that's the case). See below for a visual:
![Step Into](../images/step_into.png)

As you can see from the picture, "Force Step Into" is given the keyboard shortcut of 'Alt+Shift+F7', while the one above it, "Step Into" is given 'F7'. "Step Into" will step into literally everything, including code you did not write, like Python library code, and I find it much less useful than "Force Step Into". So we're going to switch the keyboard shortcuts for these two.

1. Right click on "Force Step Into" and then click "Remove Alt+Shift+F7"
2. Right click on "Step Into" and then click "Remove F7"
3. Right click on "Force Step Into" and then click "Add Keyboard Shortcut"
4. Click the 'F7' button, then click 'OK'
5. Right click on "Step Into" and then click "Add Keyboard Shortcut"
6. While holding the 'Alt' and 'Shift' keys click the 'F7' button, then click 'OK'
7. Click 'OK' on the main 'Settings' window and you're done!

Now, whenever you are debugging your code, you can use the familiar 'F7' keyboard shortcut to step line by line through code and step into methods and functions you wrote as well. You can follow these steps to set up all of PyCharm to have exactly the same keyboard shortcuts you remember from the VBE, such as 'F5' for running code instead of 'CTRL + Shift + F10'/"Run context configuration" and so on.

