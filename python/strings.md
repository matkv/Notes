# Strings

## String literals

String values begin and end with a single quote.

```python
'This is a string'.
```

But what if we wanted to use a single quote inside our string?

### Double quotes

One way to do it is to use double quotes instead of the single quotes. A benefit of doing that is that the string now can have a single quote in it.

```python
spam = "That is Alice's cat"
```

However, if we want to use both double quotes and single quotes, we need to use **escape characters**

### Escape characters

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