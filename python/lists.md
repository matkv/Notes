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

## Changing a list's values

```python
listname[1] = 'Hello'   #sets the second item in the list to a string value
```

We can delete values from a list using the **del** statement.

```python
del listname[2]   #deletes the third item
```

## Other list functions

* Getting the number of items in a list using the `len()` function
* Concatenating lists using the `+` operator
* Replicating lists using the `*` operator

There is also a ```list()``` function:

```python
list('Hi') #returns ['H', 'i']
```

If we need to determine whether a value is or isn't in a list we can use the **in** and **not in** operators.

```python
'Dog' in ['Cat', 'Shark', 'Dog']  #returns true
```

## Using loops with lists

```python
for i in range(4)
  print(i)
```

`range(4)` has a return value that Python considers similar to [0,1,2,3].

A common technique is to use ```(len(somelist))``` with a for loop to iterate over the indexes of a list.

## In and not operators

With the in and not operators we can check whether a value is in a list or not. These expressions evaluate to a Boolean value.

```python
if name not in myList:
  print("Not in the list)
```

## Assigning multiple values at once

```python
cat = ['fat', 'black', 'loud']
size = cat[0]
color = cat[1]
disposition = cat[2]

#Can be simplified to:
cat = ['fat' 'black', 'loud']
size, color, disposition = cat
```

To use this, the number of variables and the length of the list must be exactly equal.

## Augmented assignment operators

If we want to use the value of a variable when assigning a new value, we can use augmented assignment operators.

```python
#So instead of writing
 
 apple = apple + 1

 #We can write 

 apple += 1
```

There are augmented assignment operators for the following operations:

* +=      this can also be used for string contatenation
* -=
* *=      this can also be used for list replication
* /=
* %=

## List methods

### Finding a value in a list

We can find a value in a list with the index() method.

```python
examplelist = ['hello', 'goodbye']
examplelist.index('hello')

#this returns 0
```

When there are duplicates in a list, the first occurence is returned.