# HSE Python Advanced

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

### Sets

A set is an **unordered** container of **hashable** objects.

In Python, built-in immutable objects like strings or integers are hashable while mutable containers like lists or dictionaries are
not. Immutable containers (tuples or frozensets) are hashable if their elements are hashable.

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
print({1000, -56, 78, 9})     # {1000, 9, 78, -56}
```

