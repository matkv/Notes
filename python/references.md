# References

Varaibles store string and integer values like this:

```python
cheese = 40
milk = cheese
milk = 100

#cheese still returns 40
#milk returns 100
```

Lists don't work that way. When we assign a list to a variable, we are actually assigning a list **reference** to the variable. That is a value that points to a list. The list is always the same one, it is just referenced from two places.

```python
firstlist = [1,2,3,4,5]
secondlist = firstlist
secondlist[1] = 9

#now both firstlist and secondlist return [1,9,3,4,5]
```

Variables will contain references to list values rather than list values themselves. But for strings and integer values, variables simply contain the string or integer value. 

Python uses references whenever variables must store values of **mutable** data types, such as lists or dictionaries.

For values of **immutable** data types such as strings, integers, or tuples, Python varables will store the value itself.

## Passing references

When a function is called, the values of the arguments are copied to the parameter values. For lists and dictionaries, a copy of the reference is used.

```python
def someMethod(someParameter):
    someParameter.Append('Hello')

someList = [1,2,3]
someMethod(someList)
```

someList now returns [1,2,3, 'Hello']. By using the reference of the list, it has been modified in place. Even though someList and someParameter contain separate references, they both refer to the same list.

## The copy() and deepcopy() functions

Sometimes we might not want to change the referenced lists values and keep that original list or dictionary the way it is. For this, Python provides a module named copy that provides both the `copy()` and `deepcopy()` functions.

`copy.copy()` can be used to make a duplicate value of a mutable value (like a list or dictionary).

```python
import copy
spam = ['A', 'B', 'C', 'D']
cheese = copy.copy(spam)
cheese[1] = 42

spam
['A', 'B', 'C', 'D']
cheese
['A', 42, 'C', 'D']
```

If the list we need to copy contains other lists, we need to use **copy.deepcopy()**. This will copy the inner lists as well.