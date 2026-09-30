# Python Basics — Complete Guide

**Source repository:** [Ashraful-Momen/Web-Development-With-React-And-Django](https://github.com/Ashraful-Momen/Web-Development-With-React-And-Django/tree/main/Python/1.%20Python%20Basic)

---

## Table of Contents

| \# | Topic | File |
| --- | --- | --- |
| 1 | Basic Python | `1.Basic_Python.py` |
| 2 | Lists | `2. List_Python.py` |
| 3 | Control Statements | `3. Control_Statement_Python.py` |
| 4 | Loops | `4.Loop_Python.py` |
| 5 | Strings | `5.String_Python.py` |
| 6 | Tuples | `6.Tuples_Python.py` |
| 7 | Sets | `7.Set_Python.py` |
| 8 | Dictionaries | `8.Dictionary_Python.py` |
| 9 | Error Handling | `9.ErrorHandling_Python.py` |
| 10 | Enumerate | `10.Enumerate_Python.py` |
| 11 | Functions | `11.Function_Python.py` |
| 12 | Time & Date | `12.Time_Python.py` |
| 13 | File Handling | `13.File_Python.py` |

---

# 1. Basic Python

The very first concepts any Python programmer meets: printing, variables, math, type-casting, math functions, formatted strings, and the basic operators.

```python
# print("Hello World")
# print (2+2)
# #this is the single line Comments
# """ this is the multi line of comments"""
# print("Ashraful \n 01674317715")
# print("Ashraful \t Momen")
# print("Ashraful \"Momen\"") #\' , \"  use to print => ' or ""
```

### What this teaches

| Line | Purpose |
| --- | --- |
| `print("Hello World")` | Output text to the console. |
| `print(2+2)` | Python evaluates the expression and prints `4`. |
| `# comment` | Single-line comment — ignored by the interpreter. |
| `""" ... """` | Triple-quoted string (often used as multi-line comment). |
| `\n` | Escape sequence for a newline. |
| `\t` | Escape sequence for a tab. |
| `\\\"` / `\'` | Escape sequence to print literal `"` or `'`. |

---

## Variables

```python
# Name = "Ashraful"
# Age = 25
# CGPA = 3.88
# print("My name is "+Name)
# print(Name+ "Lives in Dhaka")
# print("His Running Cgpa is now : ",CGPA)
# print("Ashraful "+"MOMEN")
```

**Explanation**

- Variables don't need a type declaration — Python infers the type from the value.
- `+` is used both for **numeric addition** and **string concatenation**.
- A comma in `print` automatically adds a space between arguments.

---

## Math Operators

```python
# a =10
# b = 3
#
# print(a+b)   # 13
# print(a-b)   # 7
# print(a/b)   # 3.333...
# print(a*b)   # 30
# print(a**b)  # 1000   (10 to the power of 3)
# print(a%b)   # 1      (modulo — remainder)
# print(a//b)  # 3      (floor division)
```

| Operator | Name | Example | Result |
| --- | --- | --- | --- |
| `+` | Addition | `10 + 3` | `13` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `10 * 3` | `30` |
| `/` | True Division | `10 / 3` | `3.33` |
| `**` | Exponent | `10 ** 3` | `1000` |
| `%` | Modulus | `10 % 3` | `1` |
| `//` | Floor Division | `10 // 3` | `3` |

---

## Type Casting

```python
# num1 = input("Enter First Number")
# num2 = input("Enter Second Number")
#
# sum = int(num1) + int(num2)
# print("Sum is ",sum)
```

**Explanation**

- `input()` always returns a **string**.
- Wrap the value in `int()` / `float()` / `str()` to convert to the desired type before doing math on it.

---

## Math Functions

```python
# from math import *
#
# print(min(20,10))   # 10
# print(max(20,10))   # 20
# print(abs(-10))     # 10
# print(sqrt(10))     # 3.162...
# print(round(3.5))   # 4
# print(floor(3.5))   # 3
# print(ceil(3.5))    # 4
# print(exp(3))       # e^3 = 20.085...
```

`from math import *` pulls every name from the standard `math` module into the current namespace.

---

## Formatted Strings (f-strings)

```python
# a = 10
# b = 10
# print(f'{a}+{b}= {a+b}')   # 10+10= 20
```

Prefix the string with `f` and put any expression inside `{ }`.

---

## Other Operator Categories (Reference)

| Category | Operators |
| --- | --- |
| Assignment | `=`, `+=`, `-=`, `*=`, `/=`, `**=`, `&=`, `//=`, `%=` |
| Relational | `>`, `<`, `>=`, `<=`, `!=`, `==` |
| Logical | `and`, `or`, `not` |
| Identity | `is`, `is not` |

```python
# number1 = 1000000000000000000000000
# number2 = 1000000000000000000000000
#
# print(id(number1))       # memory address
# print(id(number2))
# print(number1 is number2)  # True if both IDs and values match
```

`id()` returns the memory address of the object. The `is` operator checks whether two references point to the same object.

---

# 2. Lists

A **list** is an ordered, mutable (changeable) collection that allows duplicates.

> Properties: **ordered**, **mutable / changeable**, **duplicates allowed**.

```python
# my_list = ["a","b","c", [1,3,4,],1.34,2.55]
# print(my_list)
# print(my_list[-1])   # last element
# print(my_list[-2])
# print(my_list[-3])
```

**Negative indices** count from the end: `-1` is the last item, `-2` the second-last, and so on.

---

## List Methods — Quick Reference

```python
# my_list = [1,2,3,4,5,6]
# print(dir(my_list))   # discover every method available on a list
```

| \# | Method | What it does |
| --- | --- | --- |
| 1 | `list.append(item)` | Adds an item to the end. |
| 2 | `list.pop([index])` | Removes & returns by position (default last). |
| 3 | `list.reverse()` | Reverses the list **in place**. |
| 4 | `list.insert(index, item)` | Inserts at a specific position. |
| 5 | `list.count(item)` | Counts how many times an item appears. |
| 6 | `list.remove(item)` | Removes the first occurrence of value. |
| 7 | `list.clear()` | Empties the list. |
| 8 | `list.index(value)` | Returns the position of the first match. |

---

## Changing / Removing Items

```python
# my_list[0] = "A"               # change by index
# print(my_list)
#
# vowel = ['a','e','i','o','u']
# del vowel[0]                    # delete by index
# vowel.remove('e')               # delete by value
# vowel.pop()                     # delete last
# vowel.pop(0)                    # delete by index
```

---

## Slicing `list[start:end:step]`

```python
# num = [0,1,2,3,4,5,6,7,8,9]
# print(num[:9])         # 0..8
# print(num[1:9])        # 1..8
# print(num[1:9:2])      # every other element
# print(num[-1:-11:-1])  # reversed slice
# print(num[-1::-1])     # full reversal
```

`step` of `-1` walks the list backwards. Without a `step` you must give `start > stop` for a reverse slice.

---

## Sorting

```python
# number = [3,4,65,2,8,3,4,1]
# number.sort()                  # ascending, in place
# number.sort(reverse=True)      # descending, in place
# print(sorted(number))          # ascending, returns new list
# print(sorted(number,reverse=True))
```

- `list.sort()` → mutates the original list.
- `sorted(list)` → returns a brand-new sorted list.

---

## Copying a List

```python
# number2 = number.copy()
# number2 = list(number)
# number2 = number[:]      # slicing also copies
```

All three create a **shallow copy** (the list is new, but the items inside are still references to the same objects).

---

## Joining Lists

```python
# number1 = [1,3,4,5]
# number2 = [6,7,8,9]
# marge_list = number1 + number2
#
# char = ['a','b','c']
# marge_list.extend(char)
```

`+` builds a new one; `extend` mutates the list on the left.

---

## Membership Operators

```python
# print(2 in number1)       # False
# print(2 not in number1)   # True
```

---

## Full Example — All List Methods Together

```python
furit_busket = ['apple','banana','mango']

furit_busket.append('lici')              # add at end
print(furit_busket)

furit_busket.remove('lici')
print(furit_busket)

furit_busket.insert(2,'lici')             # insert at index
print(furit_busket)

furit_busket.insert(4,'lici')
print(furit_busket)

print(furit_busket.count("lici"))        # how many 'lici'

print(furit_busket)

furit_busket2 = furit_busket.index('mango')
print(f'{furit_busket2}: index of mango')
```

---

## Custom Implementation of `list.index()`

```python
def custom_index(lst, x, start=0, end=None):
    """Find the index of the first occurrence of `x` in `lst`,
       between the optional `start` and `end` indices (inclusive)."""
    if end is None:
        end = len(lst) - 1
    start = max(start, 0)
    end   = min(end, len(lst) - 1)

    for i in range(start, end + 1):
        if lst[i] == x:
            return i
    raise ValueError(f"{x} is not in list")

# Example
my_list = [10, 20, 30, 40, 50, 30, 60]
print(custom_index(my_list, 30, 2, 5))   # -> 5
```

This shows how Python finds an item by walking the list linearly — `O(n)`.

---

# 3. Control Statements

```python
marks = 85

if marks >= 80:
    print("Grade: A+")
elif marks >= 70:
    print("Grade: A")
elif marks >= 60:
    print("Grade: B")
else:
    print("Grade: F")
```

`if / elif / else` are evaluated **top to bottom**. The first branch that is `True` runs; the rest are skipped.

---

## Nested Conditions

```python
delivery_area = ['dhaka', 'mirpur', 'kafrul', 'kazipara']
user_location = 'dhaka'
price = 800

if user_location in delivery_area:
    if price >= 800:
        print('Delivery Available and shipping charge free')
    else:
        print('Delivery charge not free')
else:
    print('Delivery not available in your area')
```

A nested `if` only runs when the outer `if` is true.

---

## Conditional Variable Scope — *the gotcha*

```python
num = 100

if num == 100:
    y = 10                  # created because condition is True

if num == 10:
    z = 20                  # NEVER created

print(y)                    # 10
# print(z)                  # NameError: name 'z' is not defined
```

Python only creates the variable if the branch that defines it actually runs.

---

## Ternary (Conditional Expression)

```python
a, b = 10, 10
max_val = a if a > 7 else b
print(max_val)              # 10

# one-liner variant:
print(a if a > 7 else b)
```

Syntax: `value_if_true if condition else value_if_false`.

---

## `assert` — Fail Fast for Debugging

```python
number = int(input("Enter any Number: "))
assert number >= 0, "AssertionError: Number must be zero or a positive integer"
print(f"Validated Input: {number}")
```

If `number < 0`, the program halts immediately with your custom message.

---

# 4. Loops

## `for` Loop — Iterating Collections

```python
fruits = ['mango', 'banana', 'jackfruit']
for x in fruits:
    print(x)
```

Syntax: `for <variable> in <iterable>`

`iterable` = any collection (list, tuple, string, range).

---

## `break` vs `continue`

```python
for x in range(1, 30):
    if 10 < x < 20:
        continue     # skip 11..19
    elif x % 2 == 0:
        print("Even Number ", x)
    elif x == 25:
        break        # exit loop entirely
    print(x)

print("Loop break")
```

| Statement | Effect |
| --- | --- |
| `continue` | Skip to the **next iteration** of the loop. |
| `break` | **Exit** the loop permanently. |

---

## Real-World Example: Budget Tracker

```python
total_price = [10, 20, 30, 500, 600]
total_budget = 1000
total_item = 0

for current_price in total_price:
    total_budget -= current_price
    if total_budget < 0:
        break
    total_item += 1

print(f"Total items purchased: {total_item}")
```

Stops buying the moment the wallet goes negative.

---

## `while` Loop

```python
i = 1
while i < 100:
    if i % 2 == 0:
        print(i)
    i += 1            # ALWAYS increment — otherwise infinite loop!
```

> ⚠️ With `while`, you must update the counter yourself — or the loop never ends.

---

## `while` + `break` / `continue`

```python
i = 0
while i < 100:
    if 18 < i < 20:
        i += 1        # increment BEFORE continue, or it spins forever
        continue
    elif i == 60:
        break
    print(i)
    i += 1

print("Loop break")
```

---

## List Comprehension — Pythonic One-Liners

```python
# long form
my_list = []
for x in range(1, 101):
    my_list.append(x)

# comprehension equivalents
another_list = [i for i in range(1, 101)]
even_list    = [x for x in range(1, 101) if x % 2 == 0]
odd_list     = [x for x in list(range(1, 101)) if x % 2 != 0]
```

Syntax: `[expression for item in iterable if condition]`

---

## Nested Loops — Multiplication Table

```python
for i in range(1, 11):
    for j in range(1, 11):
        print(f'{i} X {j} = {i * j}')
    print("------------------------------------")
```

The inner loop runs to completion for **each** step of the outer loop.

---

# 5. Strings

> A sequence of characters wrapped in `''` or `""`. **Ordered** and **immutable**.

```python
paragraph = '''This is a multi-line paragraph string.
It preserves all formatting, line breaks,
and indentation exactly as typed.'''
```

Triple quotes let a string span multiple lines.

---

## Case, Cleaning, Counting

```python
name = "   Ashraful momen"

print(name.upper())            # "   ASHRAFUL MOMEN"
print(name.lower())            # "   ashraful momen"
print(name.strip())            # "Ashraful momen" (trims whitespace)
print(name.count("a"))         # 2
```

---

## Replace

```python
new_name = name.replace("momen", "Momen Shuvo")
print(new_name)
```

Syntax: `string.replace(old, new)`.

---

## Boundary Checks, `split`, `join`

```python
word = "what, are, you, doing"

print(word.startswith("Hello"))   # False
print(word.endswith("Hello"))     # False

word_list = word.split(", ")      # ['what', 'are', 'you', 'doing']
print(word_list)

word_string = ", ".join(word_list)
print(word_string)                # "what, are, you, doing"
```

| Method | What it does |
| --- | --- |
| `startswith()` | `True/False` if string starts with the given substring. |
| `endswith()` | `True/False` if string ends with the given substring. |
| `split(sep)` | String → list, splitting on the separator. |
| `sep.join(list)` | List → string, joining with the separator. |

---

## Concatenation & Reversal

```python
firstName = "Ashraful"
lastName  = "Momen"
id_num    = 50038

greeting = " \"Welcome \" " + " " + firstName + " " + lastName + "! And your ID: " + str(id_num)
print(greeting)               #  "Welcome "  Ashraful Momen! And your ID: 50038

print(greeting[::-1])         # reverse the entire string
```

`[::-1]` is the slice trick for reversing any sequence.

---

## Formatting Techniques

```python
var   = "Momen"
value = 27
pi    = 3.14159265

# Old style
print("My name is %s" % var)
print("And Age is %d" % value)

# .format() — bracket placeholders
print("the value of pi is : {:.4f}".format(pi))   # 3.1416
print("the gravity is {} and pi {}".format(9.81, pi))
```

| Style | Placeholders |
| --- | --- |
| `%` | `%s` string, `%d` int, `%f` float |
| `.format()` | `{}`, with format spec like `:.4f` |

---

## Performance — `"".join()` vs `+`

```python
from timeit import default_timer as timer

start = timer()
my_list  = ['a'] * 100
my_join = " ".join(my_list)        # fast for large lists
stop  = timer()

print(f"Runtime duration: {stop - start} seconds")
```

> `"".join()` is dramatically faster than building with `+` in a loop.

---

# 6. Tuples

> **Ordered**, **immutable / unchangeable**, **duplicates allowed**. To mutate, convert to list with `list(tuple)`, modify, convert back.

```python
# tuple_obj = ("a",'b','c',1,32,4,[2,4,5])
# print(type(tuple_obj))
# print(tuple_obj)
# print(tuple_obj[-1])
```

---

## CRUD via `list()` ↔ `tuple()`

```python
obj = ('a','b','c')
obj = list(obj)
obj.append(1); obj.append(2); obj.append(3)
obj[0] = "A"
del obj[5]
obj.remove(2)

objTuple = tuple(obj)
print(type(objTuple), objTuple)
```

> All CRUD operations on a tuple must happen through a temporary list.

---

## Loop on Tuple

```python
furit = ("mango", "apple", "banana", "lici")
for i in range(0, len(furit)):
    print(furit[i])
```

---

## Joining & Size

```python
even = [2,4,6,8]
odd  = [1,3,5,7]
number = even + odd               # list concatenation
print(number)

import sys
print(sys.getsizeof(number), "byte")
```

---

## Tuple Unpacking with `*`

```python
i1, *i2, i3 = number

print(i1)   # first element
print(i3)   # last element
print(i2)   # everything in between (becomes a list)
```

`*i2` collects "the rest" into a new list — a feature unique to Python unpacking.

---

# 7. Sets

> **Unordered**, **unchangeable (immutable items)**, **unindexed**, **no duplicates allowed**. Items can't be changed, but you can remove & add new ones. Constructor: `set([list])` or `set(tuple)`.

```python
# fruit = {'mango', 'banana', 'watermelon'}
# print(type(fruit))
#
# basket = ('a','b','c')
# a = set(basket)
```

---

## Membership, Add, Remove

```python
fruit = {'mango', 'banana', 'watermelon'}

print("mango" in fruit)         # True

for x in fruit:
    print(x)                    # order is NOT guaranteed

fruit.add("lici")
fruit.remove("lici")            # KeyError if missing
fruit.discard("banana")         # safe — no error if missing

print(fruit.pop())              # arbitrary element
```

| Method | Behaviour when item missing |
| --- | --- |
| `remove()` | Raises `KeyError`. |
| `discard()` | Silently does nothing. |

---

## Set Algebra

```python
odd     = {1,3,5,7}
even    = {2,4,6,8}
another = {1,2,3,4,5,6,7,8}

a = odd.union(even)               # A ∪ B — no duplicates
b = odd.intersection(another)     # A ∩ B — only common
```

### Difference: `A - B`

```python
A = {1,2,3,4,5,6,7,8,9}
B = {1,2,3,10,11,12}

diff  = A.difference(B)        # in A but not B
diff2 = B.difference(A)        # in B but not A
```

### Symmetric Difference: `(A − B) ∪ (B − A)`

```python
s_diff = A.symmetric_difference(B)   # elements in either set, not both
```

### Other Set Methods

```python
A.update(B)              # A ∪= B  (mutates A)
A.intersection_update(B) # A ∩= B  (mutates A)

print(A.issubset(B))     # True if every A elem in B
print(A.issuperset(B))   # True if every B elem in A
print(A.isdisjoint(B))   # True if no element in common
```

---

## Copy & `frozenset`

```python
A = {1,2,3,4,5,6,7,8,9}
B = A                # alias (not a copy)
C = B.copy()         # shallow copy

D = frozenset([1,2,3,4,5])
# D.add(9) -> AttributeError: 'frozenset' object has no attribute 'add'
```

A `frozenset` is an **immutable set** — it supports the same algebra (union, intersection, …) but cannot be mutated.

```python
A = frozenset([1,2,3,4])
B = frozenset([3,4,5,6])

print(A.union(B))               # frozenset({1,2,3,4,5,6})
print(A.intersection(B))        # frozenset({3,4})
print(A.difference(B))          # frozenset({1,2})
print(A.symmetric_difference(B))# frozenset({1,2,5,6})
```

When you build a `frozenset` from a dict, only the **keys** are kept:

```python
person = {"name": "John", "age": 23, "sex": "male"}
fSet = frozenset(person)
print('The frozen set is:', fSet)
```

---

# 8. Dictionaries

> Key-value pairs: `dict = { key: value }`.

```python
# info = {'name':'Karan', 'age':19, 'eligible':True}
# print(info)
# print(info.keys())
# print(info.values())
```

---

## Looping Over a Dictionary

```python
# for key in info.keys():
#     print(f"The value corresponding to the key {key} is {info[key]}")
#
# print(info.items())
#
# for key, value in info.items():
#     print(f"The value corresponding to the key {key} is {value}")
```

`info.items()` returns `dict_items([('name', 'Karan'), ('age', 19), ('eligible', True)])` — pairs you can unpack.

---

## Dictionary Methods

```python
info = {'name':'Karan', 'age':19, 'eligible':True}

info.update({'age':20})          # update existing key
info.update({'DOB':2001})        # add new key
info.clear()                     # empty the dict
info.pop('eligible')             # remove by key (errors if missing)
info.popitem()                   # remove last inserted pair

del info['age']                  # delete key
info.get('name')                 # safe lookup → None if missing
```

| Method | What it does |
| --- | --- |
| `update({...})` | Add/overwrite multiple key-value pairs. |
| `clear()` | Remove everything. |
| `pop(key)` | Remove by key, return value. |
| `popitem()` | Remove and return the last inserted pair. |
| `del d[k]` | Delete one entry by key. |
| `get(key)` | Lookup that returns `None` instead of crashing. |

---

## Nested Dictionary

```python
course = {
    1: {"name": "A", "id": 101},
    2: {"name": "B", "id": 102}
}

print(course)
print(course[1]["name"])          # "A"
course[1]["id"] = 105
print(course[1]["id"])             # 105

variable = dict(zip(['key'], ['value']))   # build a dict from two iterables
```

`zip(keys, values)` is the canonical way to pair up two lists into a dict.

---

# 9. Error Handling

Use `try / except / finally` to catch errors and keep the program alive.

---

## Basic `try` / `except`

```python
# try:
#   for i in range(1, 11):
#     print(f"{int(a)} X {i} = {int(a)*i}")
# except Exception as e:
#     print("Invalid Input!")
```

## Multiple `except` Clauses

```python
try:
    num = int(input("Enter an integer: "))
    a = [6, 3]
    print(a[num])
except ValueError:
    print("Number entered is not an integer.")
except IndexError:
    print("Index Error")
```

---

## `try / except / finally`

```python
def func1():
    try:
        l = [1, 5, 6, 7]
        i = int(input("Enter the index: "))
        print(l[i])
        return 1
    except:
        print("Some error occurred")
        return 0
    finally:
        print("I am always executed")

x = func1()
print(x)
```

`finally` always runs — even on `return` or unhandled exception. That's how you guarantee cleanup (closing files, releasing locks, etc.).

---

## Granular Exception Reporting

```python
def func1():
    try:
        l = [1, 5, 6, 7]
        i = int(input("Enter the index: "))
        print(l[i])
        return 1
    except IndexError:
        print("IndexError: List index out of range!")
        return 0
    except ValueError:
        print("ValueError: Invalid input! Please enter a number.")
        return 0
    except Exception as e:
        print(f"Error occurred: {type(e).__name__} - {e}")
        return 0
    finally:
        print("I am always executed")

x = func1()
print(x)
```

`Exception as e` is the catch-all — log it for debugging but **don't**swallow it silently in real code.

---

## `raise` — Triggering Your Own Errors

```python
try:
    def voter(age):
        if age < 18:
            raise ValueError("your age is not valid for voting")
        return "you are valid for voting"
except ValueError as e:
    print("value error is printing in Here")

print(voter(17))
```

Use `raise` to enforce invariants (e.g. argument validation).

---

## Catching Multiple Errors at Once

```python
try:
    my_list = [10, 0, 3]
    ans = my_list[0] / my_list[3]   # raises either ZeroDivisionError or IndexError
    print(ans)
except (ZeroDivisionError, IndexError):
    print("Dividing by zero is not possible or index of range")
finally:
    print("Must be print this line if those error isn't handle yet!")
```

Note that `ZeroDivisionError` only triggers if the *divisor* is zero (or if the index access fails first), so the above can also raise `IndexError`.

---

# 10. Enumerate

> In JS you might use `map`/`filter`/`reduce` with index keys; in Python the equivalent is `enumerate`.

```python
marks = [12, 56, 32, 98, 12, 45, 1, 4]

for index, mark in enumerate(marks, start=1):
    print(mark)
    if index == 3:
        print("Harry, awesome!")
```

`enumerate(iterable, start=0)` returns `(index, item)` pairs. `start=1` makes the count 1-based.

Without `enumerate` you would write:

```python
index = 0
for mark in marks:
    print(mark)
    if index == 3:
        print("Harry, awesome!")
    index += 1
```

`enumerate` does the bookkeeping for you.

---

# 11. Functions

## Basic Function Definition

```python
def sum(a, b):  return a + b
def sub(a, b):  return a + b   # (note: bug in source — really a+b)
def mul(a, b):  return a + b   # ditto
def dev(a, b):  return a + b   # ditto
def display(ans):
    print("your ans is ", ans)

display(sum(2, 2))
display(sub(2, 5))
display(mul(2, 5))
display(dev(2, 9))
```

Each function takes parameters, returns a value, and the caller prints.

---

## Functions Are First-Class

```python
def large(a, b):
    if a > b:
        return a
    return b

max = large
print(max(2, 4))    # function name is just a variable
```

You can assign functions to new names, pass them as arguments, etc.

---

## `*args` — Variable Positional Arguments (Tuple)

```python
def sum(*num):
    add = 0
    for x in num:
        add += x
    print(add)

sum(20, 30)
```

`*args` packs every extra positional argument into a **tuple**.

---

## `**kwargs` — Variable Keyword Arguments (Dictionary)

```python
def student(**details):
    print(details["id"])
    print(details["name"])

student(id=101, name="Shuvo")
student(id=102, name="Ashraful", aname="Shuvo")
```

`**kwargs` packs keyword arguments into a **dictionary**.

---

## Lambda (Anonymous) Functions

```python
def suqar(x):
    return x * x

print(suqar(2))                                   # 4

cube = (lambda x: x * x * x)(2)                    # 8
print(cube)

print((lambda a, b: a*a + 2*a*b + b*b)(2, 2))      # (a+b)^2 = 16
print((lambda x: x * x)(2))                        # 4
```

`lambda parameters: expression`

---

## `map` and `filter`

```python
def square(x):
    return x * x

num = [1, 2, 3, 4]
result = list(map(square, num))             # [1, 4, 9, 16]
print(result)

ans = list(filter(lambda x: x % 2 == 0, num))  # keep evens
print(ans)                                      # [2, 4]
```

- `map(func, iterable)` → apply `func` to every element.
- `filter(func, iterable)` → keep elements where `func` returns truthy.

---

## Comprehensions as Alternatives

```python
num = [1, 2, 3, 4, 5]

result = [x * x for x in num]                 # map → list comprehension
print(result)

result = [x for x in num if x % 2 == 0]       # filter → comprehension with `if`
print(result)                                 # [2, 4]
```

Comprehensions are usually faster and more readable than `map`/`filter`.

---

# 12. Time & Date

## `time` Module

```python
import time

print(time.time())                  # seconds since the epoch (float)
print(time.ctime(time.time()))      # human-readable string
print(time.localtime(time.time()))  # struct_time in local timezone

print("I am a Line")
time.sleep(2)                       # pause for 2 seconds
print("I'm another line")           # printed 2s later
```

| Call | Meaning |
| --- | --- |
| `time.time()` | Seconds since 1970-01-01 (epoch). |
| `time.ctime(secs)` | String form of the timestamp. |
| `time.localtime(secs)` | `struct_time` in local timezone. |
| `time.sleep(secs)` | Pause execution for `secs` seconds. |

---

## Measuring Execution Time

```python
import time

start = time.time()
print(23 * 2.3)
end = time.time()
print(end - start)
```

Wrap any code between `start` and `end` to measure elapsed wall time.

---

## `datetime` Module

```python
import datetime

print(datetime.datetime.now())      # local "now"
print(datetime.datetime.utcnow())   # UTC "now"
print(datetime.date.today())        # date only

random_date = datetime.date.fromtimestamp(123456789)
print(random_date.day)
print(random_date.month)
print(random_date.year)
```

---

## `timetuple()` — Indexing Date Parts

```python
import datetime

current = datetime.datetime.now()
t = current.timetuple()

print(t[0])   # year
print(t[1])   # month
print(t[2])   # day
print(t[3])   # hour
# t[4] minute, t[5] second, t[6] weekday, t[7] yearday, t[8] DST
```

| Index | Field |
| --- | --- |
| 0 | year |
| 1 | month |
| 2 | day |
| 3 | hour |
| 4 | minute |
| 5 | second |
| 6 | weekday |
| 7 | day of year |
| 8 | DST flag |

---

## Formatting Dates

```python
from datetime import datetime

now = datetime.now()
print(now)
print(datetime.strftime(now, "%d/%m/%Y  %H:%M:%S"))
```

`strftime` = "string format time". Directives include `%d`, `%m`, `%Y`, `%H`, `%M`, `%S`, …

---

## Parsing Strings into `datetime`

```python
from datetime import datetime

book_creation_date = "03, March, 2023"
book_creation_actual_time = datetime.strptime(book_creation_date, "%d, %B, %Y")
print(book_creation_actual_time)
```

`strptime` = "string parse time". `%B` matches full month name.

---

# 13. File Handling

## Listing Files in a Directory

Three approaches — pick whichever you prefer.

### 1. `os.listdir`

```python
import os

path = "./13. File - Python"
for f in os.listdir(path):
    if os.path.isfile(os.path.join(path, f)):
        print(f"{f} is a file")
```

### 2. `os.scandir`

```python
import os

path = "./13. File - Python"
for f in os.scandir(path):
    if f.is_file():
        print(f"{f.name} is a file")
```

### 3. `pathlib`

```python
import pathlib

path = pathlib.Path("./13. File - Python")
for f in path.iterdir():
    if f.is_file():
        print(f.name)
```

---

## File Access Modes

| Mode | Meaning |
| --- | --- |
| `r` | Read (default). File must exist. |
| `r+` | Read + write. |
| `w` | Write. Truncates the file if it exists. |
| `w+` | Write + read. |
| `a` | Append. Writes after existing content. |
| `a+` | Append + read. |

---

## Reading a File

```python
# file = open('text1.txt', 'r')
# print(file.read())
# file.close()
```

### Read line by line

```python
file = open('text1.txt', 'r')
print(file.readline())
print(file.readline())
print(file.readline())
file.close()
```

### Loop with `while`

```python
file = open('text1.txt', 'r')
while True:
    line = file.readline()
    if not line:
        break
    print(line)
file.close()
```

### Use `with` — auto-closes the file

```python
with open("text1.txt", "r") as file:
    print(file.read())
```

> `with` is the recommended way — it calls `.close()` for you even on exceptions.

---

## Writing to a File

```python
# 'w' overwrites the file
with open('text1.txt', 'w') as file:
    file.write("'w' write mode: previous content vanishes")

# 'a' appends after existing content
with open('text1.txt', 'a') as file:
    my_list = ['\n this is the txt1',
               '\n this is the text 2',
               '\n this is the text 3']
    file.write("'a' append mode")
    file.writelines(my_list)
```

`writelines` does **not** add separators — you must include `\n` in each string yourself.

---

## Checking File / Folder Existence

```python
import os
print(os.path.isfile('text1.txt'))        # True/False

import pathlib
print(pathlib.Path('text2.txt').is_file())
```

---

## Deleting Files & Folders

```python
import os

# delete file
path = 'text3.txt'
if os.path.isfile(path):
    os.remove(path)
```

### Delete an empty folder

```python
import os
dir = './A'
if os.path.dirname(dir):
    os.removedirs(dir)            # empty folder only
```

### Delete a non-empty folder

```python
import os, shutil
dir_with_files = './B'
if os.path.dirname(dir_with_files):
    shutil.rmtree(dir_with_files)  # recursively deletes folder + contents
```

> ⚠️ `shutil.rmtree` is destructive and irreversible.

---

# Summary — Concepts at a Glance

| File | Big idea |
| --- | --- |
| 1 | `print`, variables, math, casting, formatting |
| 2 | Lists — order, mutate, slice, sort, search |
| 3 | `if / elif / else`, nesting, ternary, `assert` |
| 4 | `for`, `while`, `break`, `continue`, comprehensions |
| 5 | Strings — case, split/join, format, reverse |
| 6 | Tuples — immutable sequences, unpacking |
| 7 | Sets — unique, unordered, set algebra |
| 8 | Dicts — key/value, nested, methods |
| 9 | `try / except / finally`, `raise` |
| 10 | `enumerate` — index + value pairs |
| 11 | Functions, `*args`, `**kwargs`, lambdas, comprehensions |
| 12 | `time`, `datetime`, format/parse dates |
| 13 | Read/write files, directories, deletion |

Happy hacking! 🐍
