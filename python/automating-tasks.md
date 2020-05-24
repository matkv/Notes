# Automating tasks

## Pattern matching with regular expressions

Regular expressions allow us to specify a *pattern* of text to seach for. Regular expressions, called *regexes* for short, are descriptions for a pattern of text.

For example, a `\d` in a regex stands for a digit character -  a single numeral from 0 to 9. The regex ```\d\d\d-\d\d\d-\d\d\d\d``` would match a string of three numbers, a hyphen, another three numbers, another hyphen, and  four numbers.

We can make this expression even shorter: Adding a 3 in curly brackets after a pattern is like saying "Match this pattern three times".

```\d{3}-\d{3}-\d{3}``` would do the same as the above example.

## Creating Regex objects

All the regex functions in Python are in the ```re``` module. This means we need to ```import re``` to use them.

Passing a string value representing our regular expression to ```re.compile()``` returns a Regex pattern object (Regex object).

```python
phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')

#Here we are using a raw string with 'r' in order to ignore possible escape characters like \n. This makes it easier to type the regular expression.
```

## Matching regex objects

The regex object's ```search()``` method searches the string it is passed for any matches to the regex. It returns ```None``` if the regex pattern is not found in the string. If it is found, it returns a ```Match``` object. 

These objects have a ```group()``` method that will return the actual matched text from the searched string.

```python
phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
mo = phoneNumRegex.search('My number is 415-555-4242.')
print('Phone number found: ' + mo.group())
#Phone number found: 415-555-4242
```

A good online tester for regular expressions is [Regex Pal](https://regexpal.com).