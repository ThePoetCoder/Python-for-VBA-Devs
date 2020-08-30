# Filtering a Pandas Dataframe

## Two Ways Forward
There are two methods you can use to filter a Pandas DataFrame:
1. The Expression Way
2. The List Comprehension Way

I will describe both of them here, because while the expression way is much easier to understand for someone with little experience in Python, list comprehensions are an amazing Python tool that you should learn to utilize, and this is the perfect opportunity to start.

For today's lesson I will use the following toy-DataFrame:
```python
import pandas as pd

headers = ["Letters", "Even/Odd"]
python_dictionary = {
    1:  ['A', 'Odd'],
    2:  ['B', 'Even'],
    3:  ['C', 'Odd'],
    4:  ['D', 'Even'],
    5:  ['E', 'Odd'],
    6:  ['F', 'Even'],
    7:  ['G', 'Odd'],
    8:  ['H', 'Even'],
    9:  ['I', 'Odd'],
    10: ['J', 'Even'],
}

df = pd.DataFrame.from_dict(data=python_dictionary, orient='index')
df.columns = headers
```
If we were to view or print this DataFrame held in the variable `df` it would look exactly like we expect:
```
   Letters Even/Odd
1        A      Odd
2        B     Even
3        C      Odd
4        D     Even
5        E      Odd
6        F     Even
7        G      Odd
8        H     Even
9        I      Odd
10       J     Even
```
Before moving on there are a few things I want to point out about the above code:
1. Python Dictionaries and Pandas DataFrames are extremely similar and can be switched between each other at will. Here I am using the `from_dict` method of the `DataFrame` object of the `pandas` library.
2. I only added column headers to the values in the dictionary; in this case the keys (1-10) of the dictionary are seen as the index, aka the row index.
3. The `orient` parameter of the `from_dict` method can be either the string "columns" or the string "index". What it is essentially saying is "For each new entry in the dictionary, should Pandas create a new Column (`columns`) or a new Row (`index`)?" Nine times out of ten I prefer to use `orient='index'` even though by default `orient` is set to `"columns"`. If you were to switch the above code to say `orient='columns'` (and erase the naming of the columns `df.columns = headers`) the resulting DataFrame would look like this:
```python
     1     2    3     4    5     6    7     8    9     10
0    A     B    C     D    E     F    G     H    I     J
1  Odd  Even  Odd  Even  Odd  Even  Odd  Even  Odd  Even
```
Moving on...

-----
## The Expression Way
The expression way is painfully simple. Let's say we wished to filter for "Odd" in the "Even/Odd" column of the toy-DataFrame above. The expression way would look like this:
```python
df = df[df["Even/Odd"] == "Odd"]
```
As you already should know by now, in coding, syntax means a lot. The syntax of the expression way is:
```python
dataframe[dataframe[column_name] == looking_for]
```

And there you have it! A perfectly filtered Pandas DataFrame. The resulting DataFrame will look like this:
```
  Letters Even/Odd
1       A      Odd
3       C      Odd
5       E      Odd
7       G      Odd
9       I      Odd
```

-----
## The List Comprehension Way

### What are List Comprehensions
List comprehensions are a way to quickly build a list. Usually you would use a list literal or a 'for loop' to build a list, like so:
```python
>>> hard_coded_list = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J']
>>> built_at_runtime_list = []
>>> for letter in hard_coded_list:
...    letter_number = f"{letter}10"
...    built_at_runtime_list.append(letter_number)
...    
>>> built_at_runtime_list
['A10', 'B10', 'C10', 'D10', 'E10', 'F10', 'G10', 'H10', 'I10', 'J10']

```
Note on the 4th line there I have used something called an "f-string", that you can [read more about here](https://www.python.org/dev/peps/pep-0498/).
Essentially the Python code `f"{letter}10"` produces the same result as `letter + str(10)` and `"{}10".format(letter)`. In VBA it would be the same as `letter & CStr(10)`.

List comprehensions allow for the same result to be produced from fewer lines of code:
```python
>>> hard_coded_list = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J']
>>> list_comp = [f"{letter}10" for letter in hard_coded_list]
>>> list_comp
['A10', 'B10', 'C10', 'D10', 'E10', 'F10', 'G10', 'H10', 'I10', 'J10']

```

Let's break down what's happening inside that list comprehension in a little more depth:
1. We had a pre-built/hard-coded list helpfully called `hard_coded_list`
2. We wanted to tack on the number 10 to each item in the list
3. Instead of building a for loop (which in VBA and many other languages would be better understood as a "For Each" loop) we decided to build a list comprehension
4. I usually like to start out my list comprehensions with the simplest form of one; recreating the list I'm working from, which in this example would look something like this:

    `[letter for letter in hard_coded_list]`

5. Then I would modify the first variable to bring about the result I want in the final list, in this case, stick it in an f-sting:

    `[f"{letter}10" for letter in hard_coded_list]`

As you can begin to deduce from the above, the basic syntax of a list comprehension is:

```python
[result for item in iterable]
```
This is the same basic concept we had for the for loop:

```python
final_list = []
for item in iterable:
    result = edit item
    final_list.append(result)  

```

-----
### Filtering with a List Comprehension
So now that we know what a list comprehension is, we can filter a Pandas DataFrame rather simply by utilizing one.

For comparison's sake, let's filter the toy-DataFrame above, again looking for the word "Odd" in the "Even/Odd" column. 
The simplest list comprehension, to replicate the values in that column, would look like this:
```python
[value for value in df["Even/Odd"]]
```
Note the two `]]` at the end; the first one closes off the reference to the column and the second one closes the list comprehension.

Now all we need to do is come up with a `result` instead of the simply replicating each value. This is where the magic of filtering in Pandas comes from; the `result` we are looking for is a Boolean(True/False).
It would look something like this:
```python
[value == "Odd" for value in df["Even/Odd"]]
```
The result of this list comprehension is 
```python
[True, False, True, False, True, False, True, False, True, False]
```
This list of Trues & Falses will tell the DataFrame which rows stick around and which rows to filter out (Each `True` sticks around obviously).

But how do we apply it to the DataFrame? Like so:
```python
df = df[[value == "Odd" for value in df["Even/Odd"]]]
```
Note now that we have 3 `]]]` at the end!

We could also break it up to look like this:
```python
list_comp = [value == "Odd" for value in df["Even/Odd"]]
df = df[list_comp]
```
See, that's not much more difficult than the expression way.

So, with a bit of practice and careful attention to matching your square brackets `[]` you can filter any Pandas Dataframe with a list comprehension too.
