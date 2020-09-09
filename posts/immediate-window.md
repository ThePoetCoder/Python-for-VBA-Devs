# What about the Immediate Window?

PyCharm has definitely got you covered when it comes to immediate evaluation of code, and I much prefer the variety of tools they have in place of the VBE's Immediate Window.

First off, right at the bottom and left of center in the PyCharm IDE you'll see the words "Python Console". As described in the [conventions](../posts/conventions.md) the Python Console is the default way to get interactive code within Python, and PyCharm has one built right into the IDE. You can open a new console at any time and test out something quick before adding it to your codebase.

Where PyCharm really shines in this area of interactive programming is when you are in the process of debugging. Debugging can begin as simply as:
1. Adding a breakpoint (or using Python's built-in `breakpoint()` trigger function)
2. Clicking on the green bug icon next to the green 'play' triangle

Once you are debugging, you have 2 additional options available to you for immediate evaluation when stepping through code. 

### The Evaluation Window
The first one (and my favorite) is the "Evaluate" window. It can be called by pressing the keyboard shortcut `Alt + F8` or by right-clicking anywhere inside your codebase or variables in the debugger window and selecting "Evaluate Expression...". The Evaluate window is extremely powerful, and even has the ability to edit your programs variables and state while the program is running. It's main purpose (in my opinion) is for digging deep into what's going on under the hood of your program, such as if you have an object or DataFrame you need to investigate, as having whatever you're investigating in a separate window really helps keep things compartmentalized. The Evaluate window is capable of executing any valid Python code and returning the result to you in a way that can be clicked through and understood in a way the VBE could only dream of providing.

### The Debug Console
This is a separate console, available only during debugging in PyCharm, that is linked to the code that is currently running. When you start debugging, the debug window will pop up from the bottom of the screen, and you'll notice the 2 main tabs available on it are "Debugger" and "Console". The Debugger tab is the default tab and keeps track of your call stack on the left (under the word "Frames") and the variables active during the current scope / frame on the right (under the word "Variables"). The Console tab is going to be the most similar experience you'll get to working with the VBE's Immediate Window during debugging. It is similar to the Evaluate window in its power in that you can edit the value of variables while your code is running, the main difference is that you will be given results as if in a console instead of in an interactive window. Personally I make much more use out of the Evalute window than the Debug console, but to each their own!
