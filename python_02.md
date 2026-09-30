# Python for Django — Complete Guide (Files 1–12)

> Source: [Ashraful-Momen/Web-Development-With-React-And-Django](https://github.com/Ashraful-Momen/Web-Development-With-React-And-Django/tree/main/Python/2.%20Python%20for%20Django)

**Source folder:** `Python / 2. Python for Django`

---

## Table of Contents

| #  | Topic                                            | File                                  |
|----|--------------------------------------------------|---------------------------------------|
| 1  | Lists — for Django                               | `1.List_Django.py`                    |
| 2  | Tuples — for Django                              | `2.Tuple_Django.py`                   |
| 3  | Sets — for Django                                | `3.Set_Django.py`                     |
| 4  | Dictionaries — for Django                        | `4.Dictionary_Django.py`              |
| 5  | Sequence Unpacking                               | `5.Sequence_Django.py`                |
| 6  | Looping Through Sequences                        | `6.Looping through Sequences.py`      |
| 7  | Comprehensions                                   | `7.Comprehension_Django.py`           |
| 8  | Functions — `*args`, `**kwargs`, Decorators      | `8.Function-Django.py`                |
| 9  | OOP — Inheritance, MRO, Metaclasses              | `9.OOP_Django.py`                     |
| 10 | OOP Final — Encapsulation, Dunder, Properties    | `10. OOP Final in Python.py`          |
| 11 | Threading, Multiprocessing, Concurrency          | `11. Thread , Multiprocessing , Concurrency in Python .py` |
| 12 | Synchronous vs Asynchronous Programming          | `12. Synchronous vs Asynchronous Programming in Python.py` |

---

# 1. Lists — for Django

A quick refresher on the list operations you'll use most inside Django
views, serializers, and templates.

> Properties: **ordered**, **changeable / mutable**, **duplicates allowed**.

```python
my_list = ["a","b","c", [1,3,4,],1.34,2.55]
print(my_list)
print(my_list[-1])
print(my_list[-2])
print(my_list[-3])
```

**Negative indexing** counts from the end (`-1` is the last element).

---

## Mutate / Remove

```python
my_list[0] = "A"

vowel = ['a','e','i','o','u']
del vowel[0]            # by index
vowel.remove('e')       # by value (first match)
vowel.pop()             # last item
vowel.pop(0)            # by index
```

---

## Slicing `list[start:end:step]`

```python
num = [0,1,2,3,4,5,6,7,8,9]
print(num[:9])          # 0..8
print(num[1:9])         # 1..8
print(num[1:9:2])       # every other
print(num[-1:-11:-1])   # reversed slice
print(num[-1::-1])      # full reversal
```

A `step` of `-1` walks the list backwards — **without** `step` you must
give `start > stop`.

---

## Sorting

```python
number = [3,4,65,2,8,3,4,1]
number.sort()                  # in place, ascending
number.sort(reverse=True)      # in place, descending
print(sorted(number))          # returns new list
print(sorted(number, reverse=True))
```

| Form                  | Effect                          |
|-----------------------|---------------------------------|
| `list.sort()`         | Sorts the list **in place**.    |
| `sorted(list)`        | Returns a **new** sorted list.  |

---

## Copying

```python
number2 = number.copy()
number2 = list(number)
number2 = number[:]
```

All three produce a **shallow copy** (the new list is independent, but
the items inside still reference the same objects).

---

## Join / Extend

```python
number1 = [1,3,4,5]
number2 = [6,7,8,9]
merged = number1 + number2       # new list

char = ['a','b','c']
merged.extend(char)               # mutates left list
```

---

## Membership & All Methods in One Block

```python
fruit_basket = ['apple','banana','mango']
fruit_basket.append('lici')           # add at end
fruit_basket.insert(2,'lici')         # at index
print(fruit_basket.count("lici"))     # how many
print(fruit_basket.index('mango'))    # first index
```

---

## Custom `index()` Implementation

```python
def custom_index(lst, x, start=0, end=None):
    if end is None:
        end = len(lst) - 1
    start = max(start, 0)
    end   = min(end, len(lst) - 1)
    for i in range(start, end + 1):
        if lst[i] == x:
            return i
    raise ValueError(f"{x} is not in list")
```

Demonstrates how `.index()` is just a linear scan with optional bounds.

---

# 2. Tuples — for Django

> **Ordered**, **immutable**, **duplicates allowed**, **heterogeneous**
> types allowed.
> To mutate: convert with `list()` ↔ `tuple()`.

```python
tuple_obj = ("a",'b','c',1,32,4,[2,4,5])
print(type(tuple_obj))
print(tuple_obj[-1])
```

---

## CRUD via Temporary List

```python
obj = ('a','b','c')
obj = list(obj)
obj.append(1); obj.append(2); obj.append(3)
obj[0] = "A"
del obj[5]
obj.remove(2)
obj_tuple = tuple(obj)
print(type(obj_tuple), obj_tuple)
```

---

## Looping, Joining, Size

```python
fruit = ("mango", "apple", "banana", "lici")
for i in range(0, len(fruit)):
    print(fruit[i])

even = [2,4,6,8]
odd  = [1,3,5,7]
number = even + odd          # concatenate (lists, but works the same)

import sys
print(sys.getsizeof(number), "byte")
```

---

## Tuple Unpacking with `*`

```python
my_list = [1,2,3,4,5,6,7,8,9,10]

# firstVaribale, *secondVaribale, lastVariable = my_list
# *firstVaribale, secondVaribale, lastVariable = my_list
firstVaribale, secondVaribale, *lastVariable = my_list

print(firstVaribale)        # 1
print(lastVariable)         # [3,4,5,6,7,8,9,10]
print(secondVaribale)       # 2
```

The `*` collects "everything in between" into a list.

---

## Ternary Quick Note

```python
a, b = 5, 10
max_value = a if a > b else b
print(max_value)            # 10
```

---

# 3. Sets — for Django

> **Unordered**, **unchangeable (immutable items)**, **unindexed**,
> **no duplicates**. Construct via `set([list])`.

The file is essentially the same content as the Basic-Python set lesson
(file 7 of Python_01.md), with extra emphasis on `frozenset`. Below is the
quick recap plus what's new here.

```python
fruit = {'mango', 'banana', 'watermelon'}
print("mango" in fruit)

fruit.add("lici")
fruit.remove("lici")        # KeyError if missing
fruit.discard("banana")     # silent if missing
print(fruit.pop())          # arbitrary element
```

| Method     | What happens if the item is missing? |
|------------|--------------------------------------|
| `remove()` | Raises `KeyError`.                   |
| `discard()`| Does nothing — safe in any case.     |

---

## Set Algebra Recap

```python
odd = {1,3,5,7}; even = {2,4,6,8}; another = {1,2,3,4,5,6,7,8}

a = odd.union(even)                  # A ∪ B
b = odd.intersection(another)        # A ∩ B

A = {1,2,3,4,5,6,7,8,9}; B = {1,2,3,10,11,12}
diff     = A.difference(B)            # A − B
diff2    = B.difference(A)            # B − A
s_diff   = A.symmetric_difference(B)  # (A−B) ∪ (B−A)

A.update(B)              # A ∪= B
A.intersection_update(B) # A ∩= B

print(A.issubset(B))
print(A.issuperset(B))
print(A.isdisjoint({11,12,13}))
```

---

## `frozenset` — Immutable Set

```python
A = frozenset([1,2,3,4])
B = frozenset([3,4,5,6])

C = A.copy()
print(A.union(B))               # frozenset({1,2,3,4,5,6})
print(A.intersection(B))        # frozenset({3,4})
print(A.difference(B))          # frozenset({1,2})
print(A.symmetric_difference(B))# frozenset({1,2,5,6})
```

**Key rule:** a `frozenset` cannot be mutated
(`frozenset.add()` → `AttributeError`), but the same algebra still works.

> When you create a `frozenset` from a dictionary, only the **keys** are
> kept:

```python
person = {"name": "John", "age": 23, "sex": "male"}
fSet = frozenset(person)
print('The frozen set is:', fSet)
```

---

# 4. Dictionaries — for Django

Dictionaries are at the heart of Django: each model instance becomes a
dict-like object, and JSON / DRF serializers speak dictionary natively.

```python
info = {'name':'Karan', 'age':19, 'eligible':True}
print(info)
print(info.keys())
print(info.values())

for key, value in info.items():
    print(f"The value corresponding to the key {key} is {value}")
```

`info.items()` returns `dict_items([('name', 'Karan'), ('age', 19), ('eligible', True)])`.

---

## Dictionary Methods

```python
info.update({'age':20})     # overwrite existing key
info.update({'DOB':2001})   # add new key
info.clear()                # empty the dict
info.pop('eligible')        # remove by key
info.popitem()              # remove last inserted
del info['age']             # delete by key

info.get('name')            # safe lookup → None if missing
```

| Method        | Behaviour                                    |
|---------------|----------------------------------------------|
| `update({})`  | Add/overwrite multiple pairs.                |
| `clear()`     | Remove everything.                           |
| `pop(key)`    | Remove by key, return value.                 |
| `popitem()`   | Remove and return last-inserted pair.        |
| `del d[k]`    | Delete one entry.                            |
| `get(key)`    | Returns `None` instead of raising.           |

---

## Build a Dict from Two Iterables

```python
variable = dict(zip(['key'], ['value']))
print(variable)
```

`zip(keys, values)` is the canonical pairing idiom.

---

## Nested Dictionary

```python
course = {
    1: {"name": "A", "id": 101},
    2: {"name": "B", "id": 102}
}

print(course[1]["name"])
course[1]["id"] = 105
print(course[1]["id"])
```

This is exactly the shape Django returns when you serialize a related
model.

---

# 5. Sequence Unpacking

This is the one Python feature that makes Django views so compact: any
sequence (list, tuple, range) can be destructured positionally.

```python
my_list = [1,2,3,4,5,6,7,8,9,10]

firstVariable, secondVariable, *lastVariable = my_list

print(firstVariable)   # 1
print(lastVariable)    # [3,4,5,6,7,8,9,10]
print(secondVariable)  # 2
```

**The `*` collects the rest** into a new list — you can place it in any
position:

```python
firstVaribale, *secondVaribale, lastVariable = my_list
*firstVaribale, secondVaribale, lastVariable = my_list
```

---

## Useful Sequence Operators

| Operator          | Meaning                                |
|-------------------|----------------------------------------|
| `in` / `not in`   | Membership test.                       |
| `is`              | Identity (same memory location, `id()`). |

---

## Ternary / Quick Reference

```python
a = 5; b = 10
max_value = a if a > b else b
print(max_value)
```

---

# 6. Looping Through Sequences

The pattern Django uses everywhere — iterating over querysets, M2M
relations, request.POST items, etc.

```python
myTuple = ("a", "b", "c", "d")
myList  = [("a", 1, "BDT"), ("b", 2, "USD"), ("c", 3, "CAD")]
myDict  = {"name": "Simanta", "age": 26, "country": "Bangladesh"}
myStr   = "Bohubrihi"
mySet   = {"BDT", "USD", "CAD"}

for x, y, z in myList:
    print(f"{x}, {y}, {z}")

for key, value in myDict.items():
    print(f"{key} => {value}")

for ch in myStr:
    print(ch)

for currency in mySet:
    print(currency)
```

> ⚠️ **`mySet`** has no guaranteed order — iteration is unordered.

---

## `range()` and Index-Based Loops

```python
myList = list(range(1, 10))

for i in range(0, 51, 5):
    print(i)

myList = ['Spanish', 'English', 'French', 'German', 'Irish', 'Chinese']

for i in range(len(myList)):
    print(f"Language: {myList[i]}")
```

Prefer `for item in myList` when you don't need the index — it reads
cleaner.

---

## `enumerate` and `zip`

```python
myList  = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
myList2 = [1, 2, 3, 4, 5, 6]

for i, fruit in enumerate(myList):
    print(f"{i} index of {fruit}")

for i, j in zip(myList2, myList):
    print(i, j)

for i in reversed(sorted(myList)):
    print(i)
```

| Helper      | What it does                                    |
|-------------|-------------------------------------------------|
| `enumerate` | Adds a counter alongside the value.             |
| `zip`       | Walks several iterables in lockstep.            |
| `reversed`  | Iterates in reverse order (any sequence).       |

---

# 7. Comprehensions

The Pythonic way to build lists, dicts, sets, and tuples — and the
foundation for Django ORM bulk operations and DRF filtering.

---

## List Comprehension

```python
myList = [1,5,6,7,2,3]

# long form
newList = []
for i in myList:
    if i % 2 == 1:
        newList.append(i * i)

# one-liner
comList = [i**3 for i in myList if i % 2 == 1]
```

---

## Build Any Container

```python
myList = [1,2,3,4,5,6,7,8,9,10]

newList      = [i*i for i in myList if i % 2 == 0]
newDict      = {i: i*i for i in myList}                  # {1:1, 2:4, ...}
newSet       = {i**3 for i in myList}
newTuple     = tuple({i**3 for i in myList})
newTupleList = [(i, i**3, i**4) for i in myList]
```

| Target container | Syntax starter |
|------------------|----------------|
| list             | `[ ... ]` |
| dict             | `{ key: value ... }` |
| set              | `{ ... }` |
| tuple            | `tuple( ... )` |

---

## Comprehensions Over a Dict

```python
myDic = {'name': 'shuvo', 'id': 201, 'phone': 1674317715}

newList = [key   for key, value in myDic.items()]
newList = [value for key, value in myDic.items()]
newList = [(key, value) for key, value in myDic.items()]

newDict = {key + " key": value for key, value in myDic.items()}
```

---

## Comprehensions Over a String

```python
var    = "Hello bangladesh"
newStr = [i.upper() for i in var]
```

---

## Nested Comprehension — Matrices

```python
matrix = []
for i in range(3):       # row
    matrix.append([])
    for j in range(4):   # column
        matrix[i].append(j)

newMatrix = [[j for j in range(4)] for i in range(3)]

flatMatrix = [i[0] for i in newMatrix]   # first element of each row
```

---

# 8. Functions — `*args`, `**kwargs`, Decorators

## Parameters vs. Arguments

```python
# fname, lname = parameter
# argument = 'shuvo', 'momen' value.

def name(fname, lname):
    print(f"hello {fname} {lname}")

name('shuvo', 'momen')                       # positional
name(fname='shuvo', lname='momen')            # keyword
```

> **Parameters** are the names in the function definition.
> **Arguments** are the actual values passed in.

---

## `*args` — Tuple of Positional Args

```python
def anyValueTuple(*args):
    print(args)              # (True, 2, 'Bangla', 22.22, 1)
    print(args[2])

anyValueTuple(True, 2, 'Bangla', 22.22, 1)
```

---

## `**kwargs` — Dict of Keyword Args

```python
def name(**kwargs):
    print(f"hello {kwargs['fname']} {kwargs['lname']}")

name(fname='shuvo', lname='momen')

# Combining *args and **kwargs:
def name(*args, **kwargs):
    print(f"hello {kwargs['fname']} {kwargs['lname']}")
    print(args, kwargs)

name(True, 2, 'shuvo', fname='shuvo', lname='momen')
```

> Rule: **`*args` must come before `**kwargs`** in the signature.

---

## Lambda / Anonymous / IIFE

```python
def add(x, y):
    return x + y

# IIFE — Immediately Invoked Function Expression
print((lambda x, y: x + y)(10, 15))         # 25

multiplication = lambda a, b: a * b
print(multiplication(10, 2))               # 20
```

---

## `map(func, sequence)`

```python
def func(n):
    return n * n * n

l = [3, 4, 1, 0, 6]
newL = list(map(lambda n: n * n * n, l))    # [27, 64, 1, 0, 216]

l  = ['Simanta', 'Bohubrihi', 'Dhaka']
l2 = list(map(list, l))                     # [['S','i',...], ...]
```

`map` returns an **iterator**; wrap with `list()`/`set()`/`tuple()` to
materialise.

---

## `filter(func, sequence)`

```python
mylist = [3, 4, 1, 0, 6]

def func(num):
    if num % 2 == 0:
        return num * num

newList = list(filter(func, mylist))     # keep evens only
```

`filter` returns elements for which the function is truthy.

---

## `reduce(func, sequence)`

```python
from functools import reduce

myList = [1,2,3,4,5,6,7,8,9,10]

def totalSum(x, y):
    return x + y

sumOfList = reduce(lambda x, y: x + y, myList)
print(sumOfList)        # 55
```

`reduce` walks the sequence two items at a time, accumulating the result.

---

## Higher-Order Functions

```python
def higherOrderFn(fn):
    print("the function name is : ", fn.__name__)
    fn()

def hello():
    print("Hello Bangladesh")

higherOrderFn(hello)
```

A higher-order function **accepts a function as an argument** or
**returns a function**.

```python
myList = [1,2,3,4,5,6,7,8,9,10]

def newFun(fn, myList):
    newList = []
    for i in myList:
        if fn(i):
            newList.append(i)
    return newList

oddList = newFun(lambda x: x % 2 == 1, myList)
print(oddList)
```

---

## Decorators — `myWrapper` Example

```python
def myWrapper(fn):
    def test():
        print("I am from test! Before")
        fn()
        print("I am from test! After")
    return test

@myWrapper
def greet():
    print("Hello world!")

@myWrapper
def hello():
    print("Hello Hello")

hello()
```

`@myWrapper` is equivalent to:

```python
hello = myWrapper(hello)
```

| Step | What happens                                       |
|------|----------------------------------------------------|
| 1    | `myWrapper` receives the function `hello`.         |
| 2    | It defines an inner `test()` that wraps the call.  |
| 3    | Returns `test`, which replaces the original name.  |

This is how Django uses `@login_required`, `@permission_required`, etc.

---

# 9. OOP — Inheritance, MRO, Metaclasses

## Single Inheritance with `super()`

```python
class A:
    def __init__(self, name):
        self.name = name

    def display1(self):
        print(f'hello {self.name}')

    def hello():
        print("I am from A class")

class B(A):
    def __init__(self, name, job):
        super().__init__(name)         # delegate to parent
        self.job = job

    def hello(self):
        print(f"Hello I'm from B class {self.name}! You work as a {self.job}")

obj = B("shuvo", "Mentor")
obj.hello()
```

`super().__init__(name)` forwards the `name` argument to `A.__init__`.

---

## Multiple Inheritance — Method Resolution Order (MRO)

```python
class A:
    def __init__(self, name):
        self.name = name

class B:
    def __init__(self, job):
        self.job = job

class C(A, B):
    pass

obj = C('Shuvo')
print(C.__mro__)    # C → A → B → object
```

> **MRO rule:** Python walks parents left-to-right, then up. For
> `class C(A, B)`, `C` → `A` → `B` → `object`. The first class defining
> the method wins.

---

## Constructors in Multiple Inheritance

```python
class A:
    def __init__(self, name):
        self.name = name

    def hello(self):
        print("Hello I am from A class")

class B:
    def __init__(self, job):
        self.job = job

    def hello(self):
        print(f"Hello I'm from B class! You work as a {self.job}")

class C(A, B):
    def __init__(self, name, job):
        A.__init__(self, name)
        B.__init__(self, job)

    def hello(self):
        A.hello(self)
        B.hello(self)
        print(f"Hello I'm from C class! You work as a {self.job}")

obj = C("Ashraful", "Mentor")
obj.hello()
```

`super().fn()` only triggers **one** parent in MRO order. To call **both**
parents, invoke them by name (`A.__init__` / `B.__init__`).

---

## Metaclass — Every Type is a Class

```python
name   = "Ashraful"
roll   = 202
Sun    = True
myList = [1,2,3,4]
myDic  = {"name": "Shuvo"}

print(type(name))    # <class 'str'>
print(type(myList))  # <class 'list'>

class A: pass
obj = A()
print(type(obj))     # <class '__main__.A'>
print(type(A))       # <class 'type'>    <-- this is the **metaclass**
```

> A **metaclass** is the class of a class. In Python, the default
> metaclass is `type`. Every class you write is itself an instance of
> `type`. Custom metaclasses (subclasses of `type`) let you customise
> class creation.

---

# 10. OOP Final — Encapsulation, Dunder, Properties

The "everything bag" of Python OOP — this is what you need to read
Django source comfortably.

---

## 1. Classes & Objects

```python
class Car:
    total_cars = 0                       # class variable (shared)

    def __init__(self, brand, color):
        self.brand = brand               # public
        self.color = color               # public
        self._mileage = 0                # protected (convention)
        self.__vin = "123"               # private (name-mangled)
        Car.total_cars += 1

    def drive(self, distance):
        self._mileage += distance
        return f"Driving {distance} km"

    def get_vin(self):
        return self.__vin

car1 = Car("Toyota", "Red")
car2 = Car("Honda", "Blue")
print(car1.drive(100))
print(Car.total_cars)
```

### Attribute Visibility

| Form          | Name              | Access                                  |
|---------------|-------------------|-----------------------------------------|
| `self.x`      | public            | Anywhere.                               |
| `self._x`     | protected (hint)  | Discouraged outside the class.          |
| `self.__x`    | private (mangled) | Renamed to `_ClassName__x`. Hard to touch from outside. |

---

## 2. Inheritance

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def start_engine(self):
        return "Engine started"

    def stop_engine(self):
        return "Engine stopped"

class ElectricCar(Vehicle):
    def __init__(self, brand, battery_capacity):
        super().__init__(brand)
        self.battery_capacity = battery_capacity

    def start_engine(self):
        return "Electric motor started silently"     # override

    def charge(self):
        return f"Charging {self.brand}'s {self.battery_capacity}kWh battery"
```

### Multiple Inheritance

```python
class Flyable:
    def fly(self):
        return "Flying"

class FlyingCar(ElectricCar, Flyable):
    def __init__(self, brand, battery_capacity, max_altitude):
        super().__init__(brand, battery_capacity)
        self.max_altitude = max_altitude
```

`FlyingCar` inherits from both `ElectricCar` and `Flyable`. MRO resolves
conflicts.

---

## 3. Encapsulation

```python
class BankAccount:
    def __init__(self):
        self.__balance = 0

    # classic getter / setter
    def get_balance(self):
        return self.__balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            return True
        return False

    # modern getter / setter via @property
    @property
    def balance(self):
        return self.__balance

    @balance.setter
    def balance(self, value):
        if value >= 0:
            self.__balance = value
```

Use `__balance` so external code can't poke it directly. Expose read /
write access via `@property`.

---

## 4. Polymorphism & Abstract Base Classes

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): pass

    @abstractmethod
    def perimeter(self): pass

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length, self.width = length, width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * (self.length + self.width)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        import math
        return math.pi * self.radius ** 2

    def perimeter(self):
        return 2 * math.pi * self.radius
```

Anywhere a `Shape` is expected, you can pass a `Rectangle` or `Circle` —
Python only cares that `area()` / `perimeter()` exist.

---

## 5. `@staticmethod` and `@classmethod`

```python
class DateUtils:
    @staticmethod
    def is_valid_date(day, month, year):
        if month in [4,6,9,11]: return day <= 30
        if month == 2:
            return day <= 29 if year % 4 == 0 else day <= 28
        return day <= 31

    @classmethod
    def from_string(cls, date_str):
        day, month, year = map(int, date_str.split('-'))
        if cls.is_valid_date(day, month, year):
            return cls(day, month, year)
        raise ValueError("Invalid date")
```

| Decorator        | First arg  | Use when …                                  |
|------------------|------------|---------------------------------------------|
| `@staticmethod`  | none       | The method doesn't need class or instance.  |
| `@classmethod`  | `cls`      | You want to construct instances or touch class state. |

---

## 6. Magic / Dunder Methods

```python
class Point:
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __str__(self):              # str(p) → "Point(1, 2)"
        return f"Point({self.x}, {self.y})"

    def __repr__(self):             # repr(p) → "Point(x=1, y=2)"
        return f"Point(x={self.x}, y={self.y})"

    def __add__(self, other):       # p1 + p2
        return Point(self.x + other.x, self.y + other.y)

    def __eq__(self, other):        # p1 == p2
        return self.x == other.x and self.y == other.y

    def __lt__(self, other):        # p1 < p2
        return (self.x**2 + self.y**2) < (other.x**2 + other.y**2)
```

| Dunder     | Operator/Call      |
|-----------|--------------------|
| `__str__` | `str(obj)`         |
| `__repr__`| `repr(obj)`        |
| `__add__` | `obj1 + obj2`      |
| `__eq__`  | `obj1 == obj2`     |
| `__lt__`  | `obj1 < obj2`      |

---

## 7. `@property` Decorator — Computed Attributes

```python
class Temperature:
    def __init__(self, celsius=0):
        self._celsius = celsius

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperature below absolute zero!")
        self._celsius = value

    @property
    def fahrenheit(self):
        return (self.celsius * 9/5) + 32

    @fahrenheit.setter
    def fahrenheit(self, value):
        self.celsius = (value - 32) * 5/9
```

`temp.fahrenheit` reads like an attribute but is computed on demand.

---

## 8. Composition (Has-a, not Is-a)

```python
class Engine:
    def start(self): return "Engine running"
    def stop(self):  return "Engine stopped"

class CarWithComposition:
    def __init__(self, brand):
        self.brand = brand
        self.engine = Engine()    # has-an Engine

    def start_car(self):
        return f"{self.brand}: {self.engine.start()}"
```

Prefer composition over inheritance when "has-a" makes more sense than
"is-a".

---

## 9. Custom Context Manager

```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename, self.mode = filename, mode
        self.file = None

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()

with FileManager("test.txt", "w") as f:
    f.write("Hello, World!")
```

`__enter__` / `__exit__` let you use `with` on any object.

---

## 10. Descriptors

```python
class Validator:
    def __init__(self, min_value=None, max_value=None):
        self.min_value, self.max_value = min_value, max_value

    def __get__(self, instance, owner):
        return instance.__dict__[self.name]

    def __set__(self, instance, value):
        if self.min_value is not None and value < self.min_value:
            raise ValueError(f"Value cannot be less than {self.min_value}")
        if self.max_value is not None and value > self.max_value:
            raise ValueError(f"Value cannot be greater than {self.max_value}")
        instance.__dict__[self.name] = value

    def __set_name__(self, owner, name):
        self.name = name
```

A **descriptor** is any object defining `__get__`, `__set__`, or
`__delete__`. Django's `models.Field` classes are descriptors — that's
how attribute access on a model instance triggers DB lookups.

---

# 11. Threading, Multiprocessing, Concurrency

## 1. Threading — I/O-bound tasks

```python
import threading, time

def print_numbers():
    for i in range(5):
        time.sleep(1)
        print(f"Number {i}")

def print_letters():
    for letter in 'ABCDE':
        time.sleep(1)
        print(f"Letter {letter}")

t1 = threading.Thread(target=print_numbers)
t2 = threading.Thread(target=print_letters)

t1.start(); t2.start()
t1.join();  t2.join()
```

### Lock for Shared State

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance
        self.lock = threading.Lock()

    def withdraw(self, amount):
        with self.lock:                       # thread-safe section
            if self.balance >= amount:
                time.sleep(0.1)
                self.balance -= amount
                return True
            return False
```

`with self.lock:` blocks every other thread from the same `lock` until
the block exits — essential to avoid the classic "lost update" race.

---

## 2. Multiprocessing — CPU-bound tasks

```python
from multiprocessing import Process, Pool, Value
import os

def process_task(name):
    print(f"Process {name}: id {os.getpid()}")
    for i in range(3):
        time.sleep(1)
        print(f"Process {name}: Step {i}")

processes = [Process(target=process_task, args=(f"P{i}",)) for i in range(3)]
for p in processes: p.start()
for p in processes: p.join()
```

### Process Pool

```python
def calculate_square(x):
    return x * x

with Pool(processes=4) as pool:
    numbers = [1, 2, 3, 4, 5]
    results = pool.map(calculate_square, numbers)
    print(f"Squares: {results}")            # [1, 4, 9, 16, 25]
```

### Shared Counter Between Processes

```python
def increment_counter(counter):
    for _ in range(100):
        with counter.get_lock():
            counter.value += 1

counter = Value('i', 0)        # 'i' = signed int
processes = [Process(target=increment_counter, args=(counter,)) for _ in range(4)]

for p in processes: p.start()
for p in processes: p.join()

print(f"Final counter value: {counter.value}")   # 400
```

Each process gets its **own memory**; `Value` provides a shared cell.

---

## 3. Context Managers

### Class Form

```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename, self.mode = filename, mode
        self.file = None

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()
        return False              # return True to suppress the exception

with FileManager('test.txt', 'w') as f:
    f.write('Hello, World!')
```

### Decorator Form

```python
from contextlib import contextmanager

@contextmanager
def timer():
    start = time.time()
    yield
    end = time.time()
    print(f"Elapsed time: {end - start:.2f} seconds")

with timer():
    time.sleep(1)
```

`yield` is where the `with`-block runs.

---

## 4. `asyncio` — Cooperative Concurrency

```python
import asyncio

async def say_hello(name, delay):
    await asyncio.sleep(delay)
    print(f"Hello, {name}!")

async def main():
    tasks = [
        asyncio.create_task(say_hello("Alice",   2)),
        asyncio.create_task(say_hello("Bob",     1)),
        asyncio.create_task(say_hello("Charlie", 3)),
    ]
    await asyncio.gather(*tasks)

asyncio.run(main())
```

| Keyword        | Meaning                                  |
|----------------|------------------------------------------|
| `async def`    | Declares an async function (coroutine).  |
| `await`        | Yield control until the awaitable finishes. |
| `asyncio.gather`| Run several coroutines concurrently.    |

### Web Scraping with `aiohttp`

```python
import aiohttp

async def fetch_url(session, url):
    async with session.get(url) as response:
        return await response.text()

async def fetch_multiple_urls(urls):
    async with aiohttp.ClientSession() as session:
        tasks = [fetch_url(session, u) for u in urls]
        return await asyncio.gather(*tasks)
```

---

## 5. Producer / Consumer with `queue.Queue`

```python
from queue import Queue
from threading import Thread

def producer(queue):
    for i in range(5):
        time.sleep(1)
        queue.put(i)
        print(f"Produced: {i}")

def consumer(queue):
    while True:
        item = queue.get()
        if item is None:
            break
        print(f"Consumed: {item}")
        queue.task_done()

q = Queue()
prod_t = Thread(target=producer, args=(q,))
cons_t = Thread(target=consumer, args=(q,))

prod_t.start(); cons_t.start()
prod_t.join()

q.put(None)             # poison pill — stop signal
cons_t.join()
```

The **poison pill** (`None`) is the standard stop signal.

---

## 6. `ThreadPoolExecutor`

```python
from concurrent.futures import ThreadPoolExecutor

def process_item(x):
    time.sleep(1)
    return x * x

with ThreadPoolExecutor(max_workers=3) as ex:
    numbers = [1, 2, 3, 4, 5]
    results = list(ex.map(process_item, numbers))
    print(f"Results: {results}")        # [1, 4, 9, 16, 25]
```

---

## 7. `ProcessPoolExecutor`

```python
from concurrent.futures import ProcessPoolExecutor

def heavy_computation(x):
    return sum(i * i for i in range(x))

with ProcessPoolExecutor(max_workers=3) as ex:
    numbers = [1_000_000, 2_000_000, 3_000_000]
    results = list(ex.map(heavy_computation, numbers))
    print(f"Computation results: {results}")
```

Use **`ThreadPoolExecutor`** for I/O-bound, **`ProcessPoolExecutor`** for
CPU-bound.

---

# 12. Synchronous vs Asynchronous Programming

This file gives a side-by-side comparison of three execution styles for
the same task: downloading three websites.

---

## 1. Synchronous File Operations

```python
def sync_read_file():
    print("Starting file operations...")

    with open('test.txt', 'w') as f:
        f.write('Hello, World!')

    with open('test.txt', 'r') as f:
        print(f"File content: {f.read()}")

    print("File operations completed")
```

Each call **blocks** until the previous one finishes.

---

## 2. Synchronous Web Requests

```python
import requests

def sync_get_website(url):
    print(f"Getting {url}")
    response = requests.get(url)
    return f"Got {url} with status {response.status_code}, length {len(response.text)}"

def sync_get_multiple_sites():
    urls = ['http://example.com', 'http://example.org', 'http://example.net']
    results = []
    for url in urls:
        results.append(sync_get_website(url))
    return results
```

---

## 3. Synchronous Data Processing

```python
def sync_process_data(data):
    print("Processing data...")
    result = []
    for item in data:
        time.sleep(1)         # simulate I/O / CPU work
        result.append(item * 2)
    return result
```

---

## 4. Asynchronous Counterparts

```python
import aiohttp, asyncio

async def async_read_file():
    print("Starting async file operations...")
    async with aiofiles.open('test.txt', 'w') as f:
        await f.write('Hello, World!')
    async with aiofiles.open('test.txt', 'r') as f:
        print(f"File content: {await f.read()}")

async def async_get_website(session, url):
    print(f"Getting {url}")
    async with session.get(url) as response:
        text = await response.text()
        return f"Got {url} with status {response.status}, length {len(text)}"

async def async_get_multiple_sites():
    urls = ['http://example.com', 'http://example.org', 'http://example.net']
    async with aiohttp.ClientSession() as session:
        tasks = [async_get_website(session, url) for url in urls]
        return await asyncio.gather(*tasks)

async def async_process_item(item):
    await asyncio.sleep(1)             # non-blocking
    return item * 2

async def async_process_data(data):
    print("Processing data asynchronously...")
    tasks = [async_process_item(item) for item in data]
    return await asyncio.gather(*tasks)
```

> The key idiom is `asyncio.gather(*tasks)` — schedule them all, then
> wait for all of them to finish.

---

## 5. Mixing Sync and Async — Callbacks

```python
def process_result_callback(result):
    print(f"Processed result: {result}")

class DataProcessor:
    def __init__(self):
        self.callbacks = []

    def add_callback(self, callback):
        self.callbacks.append(callback)

    def process_data(self, data):
        result = data * 2
        for callback in self.callbacks:
            callback(result)
```

Real-world Django / DRF uses **signals** for the same pattern.

---

## 6. Same Task, Three Implementations

### A. Synchronous

```python
def sync_download_all():
    urls = ['http://example.com', 'http://example.org', 'http://example.net']
    results = []
    for url in urls:
        response = requests.get(url)               # blocks
        results.append(len(response.text))
    return results
```

### B. Threading

```python
from concurrent.futures import ThreadPoolExecutor

def threaded_download_all():
    urls = ['http://example.com', 'http://example.org', 'http://example.net']

    def download_url(url):
        response = requests.get(url)
        return len(response.text)

    with ThreadPoolExecutor(max_workers=3) as executor:
        return list(executor.map(download_url, urls))
```

### C. Asynchronous

```python
async def async_download_all():
    urls = ['http://example.com', 'http://example.org', 'http://example.net']

    async with aiohttp.ClientSession() as session:
        async def fetch_url(url):
            async with session.get(url) as response:
                return len(await response.text())

        tasks = [fetch_url(url) for url in urls]
        return await asyncio.gather(*tasks)
```

| Style     | Threads/Processes            | Best for                          |
|-----------|------------------------------|-----------------------------------|
| Sync      | 1                             | Trivial scripts, debugging.       |
| Threading | N OS threads (GIL shared)    | I/O-bound (HTTP, files, DB).      |
| Async     | 1 thread, many coroutines    | Many concurrent I/O connections.  |
| Multiprocessing | N OS processes (no GIL)| CPU-bound (math, transforms).     |

---

## 7. Database Operations Side-by-Side

```python
class SyncDatabaseOps:
    def get_user(self, user_id):
        time.sleep(1)
        return {'id': user_id, 'name': f'User {user_id}'}

    def get_multiple_users(self, user_ids):
        return [self.get_user(uid) for uid in user_ids]   # sequential


class AsyncDatabaseOps:
    async def get_user(self, user_id):
        await asyncio.sleep(1)
        return {'id': user_id, 'name': f'User {user_id}'}

    async def get_multiple_users(self, user_ids):
        tasks = [self.get_user(uid) for uid in user_ids]
        return await asyncio.gather(*tasks)               # concurrent
```

---

## 8. File Pipelines Side-by-Side

```python
def sync_process_files(file_list):
    results = []
    for filename in file_list:
        with open(filename, 'r') as f:
            results.append(f.read().upper())
    return results

async def async_process_files(file_list):
    async def process_file(filename):
        async with aiofiles.open(filename, 'r') as f:
            return (await f.read()).upper()

    tasks = [process_file(fn) for fn in file_list]
    return await asyncio.gather(*tasks)
```

---

## 9. Wall-Clock Comparison Driver

```python
def main_sync():
    start = time.time()
    results = sync_get_multiple_sites()
    print(f"Sync execution time: {time.time() - start:.2f} seconds")
    return results

async def main_async():
    start = time.time()
    results = await async_get_multiple_sites()
    print(f"Async execution time: {time.time() - start:.2f} seconds")
    return results

sync_results  = main_sync()
async_results = asyncio.run(main_async())
```

> Expect async to win whenever there's any waiting (network, disk). For
> pure CPU work, async has no advantage and may even add overhead.

---

# Summary — Concepts at a Glance

| File | Big idea                                                              |
|------|-----------------------------------------------------------------------|
| 1    | List CRUD, slicing, sorting, joining                                  |
| 2    | Tuples — immutable; CRUD via list, `*` unpacking                      |
| 3    | Sets & `frozenset` — uniqueness, set algebra                          |
| 4    | Dictionaries — methods, nested dicts, `dict(zip(...))`                |
| 5    | Sequence destructuring with `*rest`                                   |
| 6    | `for` over tuple/list/dict/str/set; `enumerate`, `zip`, `reversed`    |
| 7    | Comprehensions for list/dict/set/tuple; matrix flattening              |
| 8    | `*args` / `**kwargs`, lambdas, `map`/`filter`/`reduce`, decorators    |
| 9    | Inheritance, `super()`, MRO, multiple-inheritance constructors, metaclass |
| 10   | OOP pillars: encapsulation, abstraction, polymorphism, dunder, properties, descriptors |
| 11   | Threads vs processes vs asyncio; locks, pools, queues, context managers |
| 12   | Sync vs async side-by-side; same task, four implementations           |

Happy hacking! 🐍🚀
