# Select-Case Statement Workaround

Some languages (including VBA) call it a "Select-Case" statement, some languages call it a "Switch-Case" statement, but Python calls it pointless.

In general the idea is the same; have a keyword that begins the search through a series of options a variable might be, and return a value next to it. The idea is one that emphasizes clean formatting and keeping all the possibilities close to each other, but Python's solution to the problem is quite literally a series of if/elifs. The only other option is a combination of dictionaries and the get method which I will display here:

```python
default_answer = "Invalid Month Number"
months = {
        1: "January",
        2: "February",
        3: "March",
        4: "April",
        5: "May",
        6: "June",
        7: "July",
        8: "August",
        9: "September",
        10: "October",
        11: "November",
        12: "December"
    }

looking_for = 2
result = months.get(looking_for, default_answer)
print(result)  # Will print "February"

looking_for = 13
result = months.get(looking_for, default_answer)
print(result)  # Will print "Invalid Month Number"

```

If you are looking for an actual function or something along those lines you can use the below code, which makes use of [closures](https://en.wikipedia.org/wiki/Closure_(computer_programming)) to give a more general solution:
```python
def select_case_closure(dict_of_posibilities, default_answer):
    def select_case(looking_for):
        return dict_of_posibilities.get(looking_for, default_answer)
    return select_case

```

One thing to note in Python to understand what is going on in the above code is to understand the difference adding `()` makes.
If you have a method or function named/labeled in your code, you call it by adding the `()` at the end, otherwise you are simply referring to it. See below:

```python
>>> def add_2(a, b):
...    return a + b
>>> add_2(5, 10)
15
>>> add_2
<function add_2 at 0x03AC60C0>

```

With the parentheses, the result is returned, without the parentheses, the function itself is returned.
So in the case of a closure, I am actually returning a function that you can then use over and over, like so:

```python
default_answer = "Invalid Month Number"
months = {
        1: "January",
        2: "February",
        3: "March",
        4: "April",
        5: "May",
        6: "June",
        7: "July",
        8: "August",
        9: "September",
        10: "October",
        11: "November",
        12: "December"
    }

def select_case_closure(dict_of_posibilities, default):
    def select_case(looking_for):
        return dict_of_posibilities.get(looking_for, default)
    return select_case  # returning the 'select_case' function defined inside the 'select_case_closure' function

select_case_months = select_case_closure(months, default_answer)
print(select_case_months(6))  # Will print "June"
print(select_case_months(33))  # Will print "Invalid Month Number"

```

The beauty of this solution is you can reuse it over and over. Any time you need a new select-case statement, call the `select_case_closure` function and pass in a dictionary full of the possibilities and the default answer to return if one isn't found. You will be returned a unique select-case function that you can then call and pass in only what you're looking for and it will return a value from the dictionary of possibilities if it can be found or the default answer if it cannot. You can have as many variations of the returned select-case functions as you need.
