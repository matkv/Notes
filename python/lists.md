# Lists

A list is a value that contains values. It contains multiple values in an ordered sequence. A list begins and ends with square brackets and the items are separated by a comma.

Example list of strings in Python:

```python
['cat', 'dog', 'mouse']
```

A list does not necessarily need to have values of the same type in it.

## Index

In order to access an item in a list, we use an integer index.

```python
listname[0]   #the first item
```

Lists can also contain other lists. The items inside them can be accessed using mulitple indexes.

```python
listname[0][1] #first list, second item in that list
```

If we use a negative index, we count backwards from the end of the list. ```listname[-1]``` refers to the last item in the list.

## Slice

An index gets a single value from a list, a slice can get several values. The start and end are set using the a colon between them. The second index is not included.

```python
listname[1:3]   #this starts at index one and goes up to (not including) 3
```

An index returns a single value from a list, a slice returns a new list.

Leaving out the first index of a slice means it will begin at 0, leaving out the second index means the slice will go all the way to the end of the list.

```python
listname[:4]  #from start to index 4
listname[4:]  #from index 4 to end of the list
```