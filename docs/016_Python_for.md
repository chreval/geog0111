# 016 More control in Python: `for`

## Introduction

### Purpose

In this section we will learn how to add more control to our code by using loops. We will mainly be using the `for` statements for this. We will also learn about the use of `assert` statements to check our code is operating as intended.

### Prerequisites

You will need some understanding of the following:


* [001 Using Notebooks](001_Notebook_use.md)
* [003 Getting help](003_Help.md)
* [010 Variables, comments and print()](010_Python_Introduction.md)
* [011 Data types](011_Python_data_types.md) 
* [012 String formatting](012_Python_strings.md)
* [013_Python_string_methods](013_Python_string_methods.md)
* [014_Python_groups](014_Python_groups.md)
* [015_Python_control](015_Python_control.md)


## Looping with `for`

### `for ... in ...`

Very commonly, we need to iterate or 'loop' over some set of items.

The basic stucture for doing this (in Python, and many other languages) is `for item in group:`, where `item` is the name of some variable and `group` is a set of values. 

The loop is run so that `item` takes on the first value in `group`, then the second, etc. Notice in the code below that the expressions inside the loop use indentation to indicate the loop. As when we discussed indentation in `if` statements, be careful to align your statements or the code will fail.


```python
'''
for loop
'''

group = [4,3,2,1]

for item in group:
    # print item in loop
    print(item)
    
print ('blast off!')
```

    4
    3
    2
    1
    blast off!


The `group` in this example is the list of integer numbers `[4,3,2,1]`. A `list` is a group of comma-separated items contained in square brackets `[]` as we have seen before.

In Python, the statement(s) we run whilst looping (here `print(item)`) are *indented*. 

The indent can be one or more spaces, the choice is up to the programmer. You can use `<tab>` but should probably avoid it. Whatever you use, it **must be consistent**. We suggest you use 4 spaces.

It is important to note the difference between the code above and:


```python
'''
for loop
'''

group = [4,3,2,1]

for item in group:
    # print item in loop
    print(item)
    print ('blast off!')
```

    4
    blast off!
    3
    blast off!
    2
    blast off!
    1
    blast off!


In the second case, we have the `print ('blast off!')` statement inside the loop as it is indented. So it is executed each time we are in the loop. In the first case, it is outside the loop and is only run once the loop is completed.

#### Exercise 1

* generate a list of strings called `group` with the names of (some of) the items in your pocket or bag (or make some up!)
* set up a `for` loop with `group`, setting the variable `item`
* within the loop, print each value of item in turn
* at the end of the loop, print `I'm done`

Quite often, we want to keep track of the 'index' of the item in the loop (the 'item number').

One way to do this would be to use a variable (called `count` here).

Before we enter the loop, we initialise the `count` to zero. Then, within the loop, we would need to increment `count` b y one each time (i.e. add `1` to `count`):


```python
'''
for loop with enumeration
'''

group = ['cat', 'fish', '🦄', 'house']

# Before we enter the loop, we initialise the `count` to zero.
count = 0

for item in group:
    # print the count value and item
    print(f'count: {count} : {item}')
    # increment count by 1
    count += 1

```

    count: 0 : cat
    count: 1 : fish
    count: 2 : 🦄
    count: 3 : house


#### Exercise 2

* copy the code above
* check to see if the value of `count` at the end of the loop is the same as the length of the list. 
* Why should this be so?

## `range()`

If we want to use in index to count explicitly, we can use the `range()` function. The arguments of this are `(stop)`,  `(start,stop)` or `(start,stop,step)`. If not sepcified, the default values os `start` is `0`, and `step`, `1`, so `range(10)` is equivalent to `range(0,10,1)`.

The function returns an object similar to a `list` type, but known as an iterator. An iterator can be thought of as a list that returns a single item at a time. We generally use them in a for loop or similar structure. The iterator returns integers starting at `start`, up to (but not including) `stop`, in steps of `step`. 

For example:



```python
# (0,6,1) -> 0 to 6 (but not 6) in steps of 1
for i in range(6):
    print(i)
```

    0
    1
    2
    3
    4
    5



```python
# (2,10,2) -> 0 to 10 (but not 10) in steps of 2
for i in range(2,10,2):
    print(i)
```

    2
    4
    6
    8


#### Exercise 3

* use `range()` to print numbers counting down from 10 to 1 (**inclusive**)
* include comments to explain your answer

## `enumerate()`

Since counting in loops is a common task, we can use the built in method [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) to achieve the same thing as above. 

The syntax to achieve the same as the code above is then:


```python
'''
for loop with enumerate()
'''
group = ['hat','dog','keys']

for count,item in enumerate(group):
    # print counter in loop
    print(f'item {count} is {item}')

```

    item 0 is hat
    item 1 is dog
    item 2 is keys


#### Exercise 4

* copy the code above
* as in the previous exercise, check to see if the value of `count` at the end of the loop is the same as the length of the list. 
* Explain why you get the result you do

## looping over dictionaries, and `assert`

Let's set up a dictionary with the names of the months as keys, and the n umber of days in. each month as the item.

We will introduce a new term `assert` to test that the lengths of the lists are equal before we proceed. This takes the form:

    asset statement
    
If statement is `True`, the assertion passes (the code flow continues). If it is `false`, the code execution will stop at that point. It is very useful for error checking.  


```python
'''
Using the months exercise from 014_Python_groups

first construct the dictionary we want: days_in_month
'''
months = ["January","February","March","April","May",\
         "June","July","August","September","October",\
         "November","December"]
# create a list called `ndays` with the number of days in each month (for this year)
ndays = [31,29,31,30,31,30,31,31,30,31,30,31]

# now use assert to test if the lengths are equal:
# we will do that by making the statement:
#    len(months) == len(ndays)
# which can be True or False

assert len(months) == len(ndays)

# Use these two lists to make a dictionary called `days_in_month` 
# with the key as month name and value as the number of days in that month.
days_in_month = dict(zip(months,ndays))

# what are the keys
print(f'the keys are: {days_in_month.keys()}')
```

    the keys are: dict_keys(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'])


The `for ... in ...` structure we saw above applies to any group of items (or more formally, any [iterable item](https://www.w3schools.com/python/python_iterators.asp)). How could we apply this to looping over dictionaries for instance?

One straightforward way would be to simply loop over the dictionary keys:


```python
'''
loop over the keys and print key and value
'''
for k in days_in_month.keys():
    d = days_in_month[k]
    print(f'Month {k} has {d} days')
```

    Month January has 31 days
    Month February has 29 days
    Month March has 31 days
    Month April has 30 days
    Month May has 31 days
    Month June has 30 days
    Month July has 31 days
    Month August has 31 days
    Month September has 30 days
    Month October has 31 days
    Month November has 30 days
    Month December has 31 days


This works fine, but we can simplify the structure by looping over the iterable object `items()` instead of `keys(). 


```python
print(list(days_in_month.items()))
```

    [('January', 31), ('February', 29), ('March', 31), ('April', 30), ('May', 31), ('June', 30), ('July', 31), ('August', 31), ('September', 30), ('October', 31), ('November', 30), ('December', 31)]


`items()` returns a set of tuples containing (`key`, `value`). So we can directly loop over that to have the much simpler code:


```python
'''
use items
'''
for k,d in days_in_month.items():
    print(f'Month {k} has {d} days')
```

    Month January has 31 days
    Month February has 29 days
    Month March has 31 days
    Month April has 30 days
    Month May has 31 days
    Month June has 30 days
    Month July has 31 days
    Month August has 31 days
    Month September has 30 days
    Month October has 31 days
    Month November has 30 days
    Month December has 31 days


#### Exercise 5

* set up  list of numbers (years) from 2008 to 2019 **inclusive**,
* set up a list of corresponding chinese zodiac names as the items (look [online](https://www.chinahighlights.com/travelguide/chinese-zodiac/#:~:text=In%20order%2C%20the%2012%20Chinese,a%20year%20of%20the%20Rat.) for this information). 
* check that the lists have the same length
* form a dictionary from the two lists, using `dict(zip())` as in the examples above
* use `.items()` as above to loop over each year, and print the year name and the zodiac name with an f-string of the form: `f'{y} is the year of the {z}'`, assuming `y` is the key and `z` the item.
* Describe what you are doing at each step

## Summary

We should know know how to use `if` statements in Python to control program flow. We can make choices as to what happens in the code, depending on whether or not one or more tests are passed. This is a common feature of all coding languages, but it is important here that you get used to doing this in Python.

We know that conditions inside `if` statements use indentation in Python, and we know to be careful in our use of this. We have learnt about `enumerate()` and `range()`.

We have also seen the use of `assert` to do some checking that our code is correct.

There are additional notes in [docs.python.org](https://docs.python.org/3/tutorial/controlflow.html#the-range-function) you can follow up to deepen your understanding of these topics. You can get more practice with `assert` at [w3schools](https://www.w3schools.com/python/ref_keyword_assert.asp).
