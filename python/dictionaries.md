# Dictionaries

Dictionaries are a data type which provides a flexible way to access and organize data.

Unlike indexes for lists, which are only integers, indexes for dictionaries can use many different data types.

Indexes for dictionaries are called **keys**, and a key with its associated value is called a **key-value** pair. 

Dictionaries are typed with braces {}.

```python
myCat = {'size': 'fat', 'color': 'gray', 'disposition': 'loud'}
```

The dictionary's keys are `size`, `color` and `disposition`. The values for these keys are `fat`,  `gray` and `loud`. We can access these values through their keys:

```python
mycat['size']
'fat'
```

## Dictionaries vs. Lists

Dictionaries are unordered. There is no "first" item in a dictionary. Unlike lists, two dictionaries don't need to have the same order to be considered the same.

```python
eggs = {'name': 'Zophie', 'species': 'cat', 'age': '8'}
ham = {'species': 'cat', 'age': '8', 'name': 'Zophie'}
eggs == ham
True
```

Dictionaries can't be sliced like lists. Trying to access a key that does not exist in a dictionary will result in a ```KeyError``` error message.

## Methods

There are three dictionary methods that will return list-like values of the dictionary's keys, values or both.

* keys()
* values()
* items()

These returned values are not true lists, they cannot be modified and don't have an append method. But they can be used in for loops.

```python
spam = {'color': 'red', 'age': 42}

for v in spam.values():
  print(v)

  red
  42
```

items() returns tuples of the key and value.

```python
('color', 'red')
```

If we want a true list from one of these methods, we can pass its list-like return value to the `list()` function:

```python
spam = {'color': 'red', 'age': 42}
spam.keys()
dict_keys(['color', 'age']  #dict_keys value

list(spam.keys()
['color', 'age']  #actual list
```

We can use both values of `items()` in a loop like this:

```python
for k,v in spam.items():
    #do something
```

### Checking whether a key or a value exists in a dictionary

```python
spam = {'name': 'Zophie', 'age': 7}

'name' in spam.keys()
True

'Zophie' in spam.values()
True
```

If we want to check whether a value is a key in the dictionary, we can simply use the ```in``` keyword with the dictionary value itself.

```python
'color' in spam
False
```

#### The get() method

The get() method takes two arguments: the key of the value to retrieve and a fallback value to return if that key does not exist:

```python
picnicItems = {'apples': 5, 'cups': 2}

picnicItems.get{'cups', 0}
returns 2

picnicItems.get('eggs', 0)
returns 0 #key doesn't exist, fallback value has been used
```