# Strings

## String literals

String values begin and end with a single quote.

```python
'This is a string'.
```

But what if we wanted to use a single quote inside our string?

## Double quotes

One way to do it is to use double quotes instead of the single quotes. A benefit of doing that is that the string now can have a single quote in it.

```python
spam = "That is Alice's cat"
```

However, if we want to use both double quotes and single quotes, we need to use **escape characters**

## Escape characters

An escape character lets us use characters that are otherwise impossible to use in a string. It consists of a \ followed by the character we want to use.

```python
spam = 'Say hi to Bob\'s mother.'
```
**List of escape characters**

* \\' Single quote
* \\" Double quote
* \\t Tab
* \\n Newline (line break)
* \\\ Backslash

## Raw strings

A raw string completely ignores all escape characters and prints any backslash that appears in the string. To create a raw string, we place an "r" before the beginning quotation mark of a string.

```python
print(r'That is Carol\'s cat.')

#This prints "That is Carol\'s cat."
```

Python doesn't consider the backslash as a escape character.

## Multiline strings

We can use the ```\n``` character to put a newline into a string. However, it is often easier to simply use multiline strings.

They begin with three single quotes or three double quotes. Any qoutes, tabs or newlines in between the triple qoutes are considered part of the string. Python's indentation rules for blocks do not apply inside a multiline string.

```python
print('''This string
is going over multiple
lines and it works. Even single quotes like this ' work.
''')
```
The single quote, for example, does not need to be escaped.

## Multiline comments

The # character marks the beginning of a comment for the rest of the line.

If we want to write a comment that spans over multiple lines, a multiline string is often used.

```python
"""
This is a comment
that spans
over multiple lines
"""

print('Hello') #and this is normal code
```

## Indexing and slicing strings

We can use indexes and slices on strings the same way as on lists.

```python
spam = 'Hello World'

spam[0] #returns 'H'
spam[-1] # returns '!'
spam[6:] # returns 'world!'
```

This does not modify the original string. It is useful for storing parts of strings in for example a separate variable.

## The in and not operators

```python
'Hello' in 'Hello World'
#returns true

'HELLO' in 'Hello World'
#returns false

'' in 'spam'
#returns true
```

## upper(), lower(), isupper() & islower()

When applied to a variable holding a string, the upper()/lower() methods return a string with all uppercase or lowercase letters. They do not change the original string, to change it, we have to set the variable specifically.

```python
spam = 'hello'
spam = spam.toupper()

#spam now returns 'HELLO'
```

This is useful if we want to make case-insensitive comparisons.

The ```isupper()``` and ```islower()``` return true if the string has at least one letter and all of its letters are uppercase/lowercase.

```python
spam = 'Test'
spam.islower()  #returns false

spam = 'test'
spam.islower() #returns true

spam = '12345'
spam.isupper()  #returns false, no letters
```

## isX string methods

Several other string method's that check whether a string matches a certain condition:

* ```isalpha()``` returns true if a string consists only of letters and is not blank.
* ```isalnum()``` returns true if a string consists only of letters and  numbers and is not blank.
* ```isdecimal()``` returns true if a string consists only of numeric characters and is not blank.
* ```isspace()``` returns true if a string consists only of spaces, tabs and newlines and is not blank.
* ```istitle()``` returns true if a string consists only of words that begin with an uppercase letter followed by only lowercase letters.

These methods are helpful when we need to validate user input, for example.

## startswith() and endswith()

These two methods return true if the string starts/ends with the string passed into the method.

```python
'Hello world!'.startswith('Hello')

#returns True
```

## join() and split()

The join() method is called on a string, takes a list of string as arguments and returns a string. The returned string is the concatenation of each string in the passed list.

The string on which it is called on is inserted between each string in the list argument.

```python
', '.join(['cats', 'rats', 'bats'])

#returns 'cats, rats, bats'
```

The split() method does the opposite. It's called on a string value and returns a list of string. By default, the string is split wherever whitespace characters (space, tab or newline) appear.

```python
'Hi hello goodbye'.split()

# returns ['Hi', 'hello', 'goodbye']
```

However, we can pass a specific string on which the string should be split.

```python
'MyABCnameABCisABCSimon'.split('ABC')
#returns ['My', 'name', 'is', 'Simon']
'My name is Simon'.split('m')
#returns ['My na', 'e is Si', 'on']
```

A common use of split() is to split a multiline string along the newline characters ('\n').

## Justifying text with rjust(), ljust() and center()

These methods return a padded version of the string they are called on with spaces inserted to justify the text. The first argument is an integer length for the justified string.

```python
'Hello'.rjust(10)

#returns '    Hello'
#total string length is 10
```

An optional second argument specifies the fill character.

```'Hello'.rjust(20, '*')``` will return a 20 character long string that starts with '*' characters.

The center() method does the same as ljust() or rjust() - but it centers the string.

Using these methods lets us ensure that stirngs are neatly aligned, even if we don't know how many characters long the strings are.

## Removing whitespace with strip(), rstrip() and lstrip()

```python
spam = '        Hello World       '
spam.strip()
'Hello World'
spam.lstrip()
'Hello World        '
spam.rstrip()
'        Hello World'
```

Optionally, we can pass a string argument to specify which characters on the ends should be stripped.

```python
spam = 'SpamSpamBaconSpamEggsSpamSpam'
spam.strip('Spam')
#returns 'BaconSpamEggs'
```

## Copying and pasting strings with the pyperclip module

```python
import pyperclip
pyperclip.copy('Hello world!')
pyperclip.paste()
#pastes 'Hello world!'
```

If something outside our program changes the clipboard contents, the paste() function will return it.