# Getting a Row Count

Getting a count of the number of rows in a pandas Dataframe is very simple, and most of the time is a lot easier than in VBA. In VBA you have to use one of [a number of workarounds](https://www.thespreadsheetguru.com/blog/2014/7/7/5-different-ways-to-find-the-last-row-or-last-column-using-vba) that logically seem like they have to bounce around the page to get an answer:
```vb
LastRow = ws.Cells(ws.Rows.Count, "A").End(xlUp).Row

```

What that bit of code is actually conveying is "give me the row of the first cell you bump into when you're going up the spreadsheet from the last possible row". Which makes sense, but is definitely a hassle to remember or understand more than believing, copying, and pasting it.

Pandas, by virtue of not starting off with a giant worksheet where anything can be put into any cell, can simplify this problem down to a single `len` function:
```python
last_row = len(df.index)

```

By the time you have a DataFrame object, the size of the data is already determined. And the index of the DataFrame object is a group of unique references to each row. By default, they are zero-based numbers, kind of like the row headings on the left of a worksheet, and the length of that index is equal to the number of rows in your DataFrame!

There are problems you can run into with this approach if, for example, you are importing this DataFrame from an Excel worksheet that has a messy layout, with content in cells below the last row you wanted to extract, but the solution to that is going to be individual to each problem set and beyond the scope of this post. I will go into cleansing data in pandas in future posts.
