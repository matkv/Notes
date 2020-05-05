# Data types
## List-like types: Strings & tuples

We can consider a string a "list" of single text characters. Many of the methods that are used on lists can be used on strings:

* indexing
* slicing
* for loops
* len()
* in and out operators

## Mutable and immutable data types

But lists and strings are different datatypes. A list is a **mutable** datatype - it can have values added, removed or changed. A string is **immutable**. It cannot be changed.

The only way to "mutate" a string is to use slicing and concatenation to build a new string out of the old string. In this example the string is not actually modified, we just pick the parts we need from the old string and create a new string:

```python
name = 'Zophie a cat'
newName = name[0:7] + 'the' + name[8:12]

#newName now returns 'Zophie the cat'
```

In the following example, the values of the list are not changed, but a new and different list value is overwritten over the old one:

```python
eggs = [1,2,3]
eggs = [4,5,6]
```

If we were using methods like append() or del(), we would be actually modifying the old list, because those changes would happen *in place* - the value is not replaced with a new value.

## Tuples

Tuples are almost identical to a list, except two differences:

* Tuples are typed with parentheses -> ```eggs = ('hello', 42, 0.5)```
* They are **immutable**

If we only have one value but we want to indicate that we are using a tuple, we can just add a trailing comma:

```python
test = ('hello',) #this is a tuple
test = ('hello')  #this is a string
```

We can use tuples to make people reading our code understand that we don't intend for these values to change. Python can also use some optimizations to make using tuples a bit faster than lists.

We can convert from lists to tuples and vice versa using the **list()** and **tuple()** functions.