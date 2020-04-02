# Functions

## Built-in functions

All Python programs can call a basic set of functions calle **built-in functions**. For example ```print()```, ```input()``` or ```len()```.

Python also comes with a set of modules called the **standard library**. Each module is a Python program that contains a related group of functions that can be used in our programs. For example ```math``` module or the ```random``` module.

First we must import the module, then we can look for a function inside the module by using the module name + dot.

```python
import random 
random.randint(1, 10)
```

We can import multiple modules in one statement. An alternate form of import would be this:

```python
from random import *
```

Modules that don't come directly with Python are called **third party modules**. We can install them using the **pip** program which comes with Python.