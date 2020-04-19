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

## Writing your own functions

Example function:

```python
def hello(name):
  print('Howdy' + name)
```

* Argument -> variable between parentheses at function call
* Parameter -> variable between parentheses at function declaration

Function calls can be part of expressions because the **evaluate to a value** returned by the function. **Every** function call has a return value. In the function declaration we can specify the type of the return value.

```python
def plusOne(number):
  return number + 1
```

The return value **None** is a value of datatype None which is a datatype to describe a value that represents the lack of a value. If our function doesn't have a return statement, the return value defaults to the None type.

There are optional **keyword** arguments that let us set specific options in functions. For example, the ```end``` keyword of the ```print()``` function specifies the character that is added at the end of the value that is printed.

## Global and local scopes

A scope is basically a container of variables. The global scope is **outside** of functions, each function has its own local scope.

* Variables that are **assigned in a function** exist in that local scope. 
* Variables that are assigned out of all functions exist in the global scope.
* A variable can't be both local and global.
* A local scope is created whenever a function is called & destroyed when the function returns
* Global variables **can be accessed from anywhere**, local variables **only within the local scope**.
* To assign a global variable inside a function we can use the ```global```  keyword.

```python 
eggs = 'Hi'

def example()
  global eggs
  eggs = 'Hello'
  print(eggs)
```

```eggs``` in this function will always refer to the **global** variable, so this will print "Hi"

## Handling errors with try/except

We can handle errors by using try and except statements.

```python
def div42by(divideBy):
    try:
        return 42 / divideBy
    except ZeroDivisionError:
        print('Error: you tried to divide by zero!')
```

An error that happens inside the try block will cause the except block to execute. We can catch specific exceptions by specifying the exact exception name. 

It is possible to catch all exceptions by just not specifyng a specific type of exception and just using "except:", but this is generally not recommended.

We can also use:

```python
 except Exception:
```

The advantage of this over the bare except is that there are a few exceptions that it wont catch, most obviously KeyboardInterrupt and SystemExit.