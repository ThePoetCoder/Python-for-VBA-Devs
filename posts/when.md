# When is it Time to Move on from VBA?

VBA gets a bad rap from Software Engineers sometimes for a variety of reasons:
* It's not the most powerful language out there
* It's not a general purpose language (the use case is very limited)
* It's been declared legacy (no new updates) by Microsoft since 2008 (for context that's a year before the world knew what an iPad was! We've come a long way since then)
* No version control
* No built-in ability to test your code, unit testing or otherwise
* Sharing it with your users is often a pain point (they can have macros disabled for example)
* A lot of people who don't know what they're doing with it can make big mistakes

The list goes on and on, and yet millions of dollars in business decisions still depend on it. So what gives? And when should you reach for another tool or language (like Python) to add to your repertoire? 

## What I feel Microsoft **really** got right with VBA is it's limited use-case and ease of use.

### Limited Use Case
With VBA, the use case is immediately obvious; it's used for Excel or other Microsoft Office Applications. It says so right in it's name "Visual Basic **for Applications**". And while this is perfect if all the things you want to automate are also inside Microsoft Office Applications, eventually you're going to outgrow that sandbox, the same way you outgrew functions and Ribbon buttons and had to move on to VBA.

### Ease of Use
There's no denying that VBA is easy to learn and use. It's likely your first subroutines were even built with the Macro recorder! How awesome is that? It writes code for you! And once you need to dive into the code, the object model has a very logical hierarchy (for Excel it's Application -> Workbook -> Worksheet -> Range, etc.) and between the macro recorder and some trial and error you can figure out how to read and edit your code.

### When to Make the jump to Python
Python is just about as easy to learn as VBA (no macro recorder but a very logical language structure). With Python however you get a lot more freedom to pick your own use case, and with that comes a lot more questions. Python can work with spreadsheets as well as it can work with just about anything. You can do things with Python you wouldn't even dream of doing in VBA, but you need to readjust your scope of what's possible in order to think up an idea of what to do in the first place. 

Here are some questions you can ask yourself that indicate you're reaching the edge of the Excel / VBA sandbox: 
* Have you ever wanted to run one of your macros without opening Excel first? Where something that could feasibly be 1 button push becomes 3-4 buttons when you consider opening Excel, opening a blank workbook, clicking on the right tab, running the macro, etc. 
* Do you need to reach for PowerQuery every day to get the job done?
* Is your VBA littered with API calls and PtrSafe stuff to temporarily reach outside the sandbox and accomplish what you have in mind?

Answering 'yes' to any of these questions is an indication you are outgrowing VBA as a language and Excel as a tool. To start down the path of learning what is possible in Python check out [this link](https://automatetheboringstuff.com). It is very beginner friendly, and Python goes way deeper than this describes, but as a first place to dive in it's very helpful.
