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