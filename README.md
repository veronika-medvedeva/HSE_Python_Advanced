# HSE Python Advanced

* [Variables, referenses and mutability](#variables-references-and-mutability)
* [Hash](#hash)
* [Sets](#sets)
* [Dictionaries](#dictionaries)
* [Sorting](#sorting)

## Variables, referenses and mutability

### Mutable vs. Immutable Objects

“Not all objects are created equal”

There are two kinds of objects in Python: Mutable objects and Immutable objects. The value of a mutable object can be modified in place after it’s
creation, while the value of an immutable object cannot be changed.

* **Immutable** Object: int, float, long, complex, string tuple, bool

* **Mutable** Object: list, dict, set, byte array, user-defined classes

Let’s see what happens when we apply id() on an immutable object, an integer:
```
a = 89
id(a) -> 4434330504

a = 89 + 1
print(a) -> 90

id(a) -> 4430689552 # this is different from before!
```
..and contrasting the result with a mutable object, a list:
```
L = [1, 2, 3]
id(L) -> 4430688016

L += [4]
print (L) -> [1, 2, 3, 4]

id(L) -> 4430688016 # this is the same as before!
```
### Making References to Values

Each time we create a variable that refers to an object, a **new** object is created.
```
L1 = [1, 2, 3]
L2 = [1, 2, 3]
L1 == L2 -> True        # L1 and L2 have the same value

L1 is L2 -> False       # L1 and L2 do not refer to the same object!
```
We can, however, have two variables refer to the same object through a process called **aliasing**: assigning one variable the value of the other
variable. In other words, one variable now serves as an alias for the other, since both of them now refer to the same object.
```
L1 = [1, 2, 3]
L2 = L1                 # L2 now refers to the same object as L1
L1 == L2 -> True

L1 is L2 -> True

L1.append(4)
print (L2) -> [1, 2, 3, 4]
```
Since L1 and L2 both refer to the same object, modifying L1 results in the same change in L2.

### Create copy

To create separate copy of mutable object:
```
import copy
c = [1, 2, 3]
f = copy.deepcopy(c)
f.append(10)
print(c) -> [1, 2, 3]
```
## Hash

* **hash** function is any function that can be used to map data of arbitrary size to fixed-size values. 
* values returned by a hash function are called **hash values**, hash codes, digests, or simply hashes. 
* values are usually used to index a fixed-size table called a **hash table**.

## Sets

A set is an **unordered** container of **hashable** objects.

In Python, built-in immutable objects like strings or integers are hashable while mutable containers like lists or dictionaries are
not. Immutable containers (tuples or frozensets) are hashable if their elements are hashable.

### +
* fast search
* remove duplicates

### -
* unordered container
* no mutable objects

A set can be created in different ways:
```
set_0 = set()                                             # empty set
set_1 = {3.14, 7.07, 2.718}                               # set of float numbers
set_2 = {1, 2.37, 'le-7'}                                 # set of objects with different types
set_3 = set(['hello’, 'world'])                           # set from iterable object
set_4 = set('Hello')                                      # {'H', 'e', 'l', 'o'}
set_5 = set(range(10))                                    # {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
set_6 = {x for x in [1, 6, 3, 8, 9]1}                     # set comprehension
set_7 = {x for x in range(10) if x % 2 == 0}              # +filtration, {0, 2, 4, 6, 8}
```
complex filtration
```
set_8 = {x for x in range(20) if x % 2 == 0 and x % 3 == 0} # {0, 6, 12, 18}
```
for complex expressions, this formatting is preferable:
```
set 9 = {
         x**2                            # expression
         for x in range(20)              # source
         if x % 2 == 0 and x % 3 == 0    # predicate
         }
```
The order of elements in the set can be random.
```
print({1000, -56, 78, 9}) # {1000, 9, 78, -56}
```

### Operations with set

len(s)
* Return the number of elements in set s (cardinality of s)
```
len({'hello', 'world'}) -> 2
```
x in s 
* Test x for membership in s
```
1 in {1, 2, 3} -> True
0 in {1, 2, 3} -> False
```
x not in s 
* Test x for non-membership in s

s.add(x) 
* Add element x to the set
```
numbers = {7, 4, 2, 4}
numbers.add(5)
print(numbers) -> {2, 4, 5, 7}

numbers.update({0, 1, 2})
print(numbers) -> {0, 1, 2, 4, 5, 7}
```
s.remove(x) 
* Remove element x from the set. Raises KeyError if x is not contained in the set

s.discard(x) 
* Remove element x from the set if it is present

s.pop() 
* Remove and return an arbitrary element from the set. Raises KeyError if the set is empty
```
numbers = {7, 4, 2, 4, 1, 3, 8}
numbers.remove(4) -> ok
numbers.discard(1) -> ok

numbers.remove(5) -> KeyError: 5
numbers.discard(6) -> ignore
print(numbers) -> {2, 3, 7, 8}
```
s.copy() 
* Return a new set with a shallow copy of s

s.clear() 
* Remove all elements from the set
```
numbers.clear()
print(len(numbers)) -> 0
```
### Operations with two sets

**s==t**
* Test sets to equality
```
{1, 3, 2} == {1, 2, 1, 3, 2}  # True
{1, 3, 2} == {1, 2}           # False
```
**s<=t** and **s.issubset(t)**
* Test whether every element in s is in t

**s<t** and **s<=t** and **s!=t**
* Test whether s is a proper subset of t
```
{1, 2} < {1, 2, 3}            # True
```
**s>=t** and **s.issuperset(t)**
* Test whether every element in t is in s

**s>t** and **s>=t** and **s!=t**
* Test whether s is a proper superset of t

**s|t** and **s.union(t)**
* Return a new set with elements from s and t
```
{1, 2, 3, 4} | {2, 4, 5, 6} # {1, 2, 3, 4, 5, 6}
```
**s&t** and **s.intersection(t)**
* Return a new set with elements common to s and t
```
{1, 2, 3, 4} & {2, 4, 5, 6}  # {2, 4}
```
**s-t** and **s.difference(t)**
* Return a new set with elements in s that are not in t
```
{1, 2, 3, 4} - {2, 4, 5, 6}  # {1, 3}
```
**s^t** and **s.symmetric_difference(t)**
* Return a new set with elements in either s or t but not both
```
{1, 2, 3, 4} ^ {2, 4, 5, 6}  # {1, 3, 5, 6}
```
**s|=t** and **s.update()**
* Update s, adding elements from t

**s&=t** and **s.intersection_update(t)**
* Update s, keeping only elements found in it and t

**s-=t** and **s.difference_update(t)**
* Update s, removing elements found in t

**s^=t** and **s.symmetric_difference_update(t)**
* Update s, keeping only elements found in either set, but not in both

Note: some methods may accept multiple iterable objects (not only sets).
```
s = {1, 2}
t = s.union((3, 4), [5, 6] , {7, 8, 9})
print(t) # {1, 2, 3, 4, 5, 6, 7, 8, 9}
```
## Dictionaries

A **dictionary** is used to store a mapping from one set of objects to another. An entry in a dictionary consists of a key and its associated value. Values can be any type of object, but keys must be hashable.

A **dict** can be created in different ways:

empty dict
```
dict_0 = dict()
```
standard initialization
```
dict_1 = {'USA': 2, 'France': 2, 'Germany': 1}
```
from list of tuples
```
dict_2 = dict([('USA', 2), ('France', 2), ('Germany', 1)])
```
from mix of lists and tuples
```
dict_3 = dict((('USA', 2), ('France', 2), ['Germany', 1]))
```
this is correct too
```
dict_4 = dict(USA=2, France=2, Germany=1)
```
dict comprehension
```
countries = ['USA', 'France', 'Germany']
counts = [2, 2, 1]
dict_5 ={
         countries[i]: counts[i]
         for i in range(len(countries))
         if counts[i] > 1
         }
```
### Operations with dict:

**len(d)**
* Return the number of items in the dictionary d

**key in d**
* Return True if d has a key, else False

**del d[key]**
* Remove d[key] from d. Raises a KeyError if key is not in the dict

**d.pop(key[, default])**
* If keyis in the dictionary, remove it and return its value, else return default. If default is not given and key is not in the dictionary, a KeyError is raised

**d.clear()**
* Remove all items from the dictionary d

**d.copy()**
* Return a shallow copy of the dictionary d

Iterate through a dictionary:

keys
```
for key in d: pass
for key in d.keys(): pass
```
values
```
for value in d.values(): pass
```
pairs of key and value
```
for key, value in d.items(): pass
```
### Dictionaries - extra methods

**get(key [, default])**
* Return the value for key if key is in the dictionary, else default. If default is not given, it defaults to None, so that this method never raises a KeyError.

**update([other])**
* Update the dictionary with the key/value pairs from other, overwriting existing keys. Return None

**setdefault(key [, default])**
* If key is in the dictionary, return its value. If not, insert key with a value of default and return default, default defaults to None.

## Sorting

Python lists have a built-in **list.sort()** method that modifies the list in-place. There is also a **sorted()** built-in function that builds a
new sorted list from an iterable.

A simple ascending sort is very easy: just call the sorted() function. It returns a new sorted list:
```
sorted([5, 2, 3, 1, 4) -> [1, 2, 3, 4, 5]
```
You can also use the list.sort() method. It modifies the list in-place (and returns None to avoid confusion). Usually it's less
convenient than sorted() - but if you don’t need the original list, it’s slightly more efficient.
```
a = [5, 2, 3, 1, 4]
a.sort()
a -> [1, 2, 3, 4, 5]
```
Another difference is that the list.sort() method is only defined for lists. In contrast, the sorted() function accepts any iterable.
```
sorted({1: 'D', 2: 'B', 3: 'B', 4: 'E', 5: 'A'}) -> [1, 2, 3, 4, 5]
```
### Key Functions

Both list.sort() and sorted() have a key parameter to specify a function to be called on each list element prior to making
comparisons.

For example, here's a case-insensitive string comparison:
```
sorted("This is a test string from Andrew".split(), key=str.lower) 
-> ['a', 'Andrew', 'from', 'is', ‘string’, 'test', 'This']
```
The value of the key parameter should be a function that takes a single argument and returns a key to use for sorting purposes.
This technique is fast because the key function is called exactly once for each input record.

A common pattern is to sort complex objects using some of the object's indices as keys. For example:
```
student_tuples = [
# (name, grade, age)
('john', 'A', 15),
('jane', 'B', 12),
('dave', 'B', 10),

sorted(student_tuples, key=lambda student: student[2]) # sort by age
-> ('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```
### Operator Module Function

The key-function patterns shown above are very common, so Python provides convenience functions to make accessor functions easier and faster. The operator module has **itemgetter()** function.
```
from operator import itemgetter
sorted (student_tuples, key=itemgetter(2))
-> [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```
The operator module function allow multiple levels of sorting. For example, to sort by grade then by age:
```
sorted (student_tuples, key=itemgetter(1, 2))
-> [('john', 'A', 15), ('dave', 'B', 10), ('jane', 'B', 12)]
```
#### Ascending and Descending

Both list.sort() and sorted() accept a reverse parameter with a boolean value. This is used to flag descending sorts. For example, to get the student data in reverse age order:
```
sorted (student_tuples, key=itemgetter(2), reverse=True)
-> [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
```
### Sort Stability

Sorts are guaranteed to be stable. That means that when multiple records have the same key, their original order is preserved.
```
data = [('red', 1), ('blue', 2), ('red', 2), ('blue', 1)]
sorted(data, key=itemgetter(0))
-> [('blue', 2), ('blue', 1), ('red', 1), ('red', 2)]
```
