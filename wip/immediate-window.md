# What about the Immediate Window?

PyCharm has definitely got you covered when it comes to immediate evaluation of code, and I much prefer the variety of tools they have in place of the VBE's Immediate Window.

First off, right at the bottom and left of center in the PyCharm IDE you'll see the words "Python Console". As described in the [conventions](../posts/conventions.md) the Python Console is the default way to get interactive code within Python, and PyCharm has one built right into the IDE. You can open a new console at any time and test out something quick before adding it to your codebase.

Where PyCharm really shines in this area of interactive programming is when you are in the process of debugging. Debugging can begin as simply as:
1. Adding a breakpoint (or using Python's built-in `breakpoint()` trigger function)
2. Clicking on the green bug icon next to the green 'play' triangle

Once you are debugging, you have 2 additional options available to you for immediate evaluation when stepping through code. 

### The Evaluation Window
The first one (and my favorite) is the "Evaluation Window"***. It can be called by pressing the keyboard shortcut `Alt + F8` or by right-clicking anywhere inside your codebase and selecting "Evaluate Expression"***. This window is extremely powerful, and has the ability to edit your programs variables and state while it is running***. It's main purpose is for digging deep into what's going on under the hood of your program, such as if you have an object or Dataframe you need to investigate, as having it in a separate window really helps keep things compartmentalized. It is, however, perfectly capable of executing any valid Python code.