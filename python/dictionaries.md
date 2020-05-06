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

### Methods

//TODO