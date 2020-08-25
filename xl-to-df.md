# Importing Data From Excel

The Pandas library is a shockingly powerful tool, and much like Excel allows you to get started immediately using the most basic features and take advantage of more and more powerful features as you progress in both your understanding of the library, your general Python skills, and the different ways you'll begin to think about data and how to get what you want with a powerful new tool in your arsenal.
While there are many other libraries that can handle importing from and creating Excel files, Pandas is a wonderful choice and my personal favorite.

Here is the easiest way I've found to get data out of Excel and into Pandas:
```python
import pandas as pd
filepath = r"C:\Absolute\path\to\your\file.xlsx"

# If you need to reference a particular worksheet
df = pd.read_excel(filepath, sheet_name="Sheet2")

# If there is only 1 worksheet in the workbook
df = pd.read_excel(filepath)

```

Let's break this down line by line:

`import pandas as pd`:
    This is what you'll see most people write to import pandas. The `as` keyword is simply a way to shorten the library's name to 2 characters instead of 6. You could just as easily write `import pandas`, but every time you want to reference it later in the code you would have to write out the entire library name instead of a 2-letter abbreviation. Yea, programmers can be lazy...

`filepath = r"C:\Absolute\path\to\your\file.xlsx"`:
    I'm creating a variable named `filepath` and storing a string in it that is the full filepath to my Excel workbook, including the extension. Pandas works equally well with '.xlsx', '.xls', & '.xlsm' extensions. Please note the letter "r" in front of my opening quote; this is how you signify to Python you want to interpret the string in its 'Raw Format', which basically means 'use exactly what is typed here instead of interpreting special characters to mean something they're not'. Here I am using it to disregard the escape character, "\\", as Python would interpret that inside a string to mean something other than the simple delimiter between folders & files that I want it to mean. I could have also simply switched all the "\\" to "/" and Pandas would have had no problem understanding what I mean there either.

`df = pd.read_excel(filepath, sheet_name="Sheet2")`: 
    The `pd` library we imported is being called finally, and a method that is helpfully named `read_excel` is being called from it. I pass the filepath variable we created earlier as the first parameter & "Sheet2" as the 2nd parameter. This allows me to specifically reference a sheet other than the 1st/default sheet in that workbook".

`df = pd.read_excel(filepath)`:
    Alternatively, if you want to reference the default sheet in a workbook, or there is only 1 sheet to begin with, then you can leave the `sheet_name` parameter off.
    
And that's it. You have now created your first Pandas Dataframe in the variable `df`.

