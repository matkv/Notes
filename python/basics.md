# Python

Python is a high level, interpreted, general-purpose programming language. Its design pilosophy emphasizes **code readabilty** and supports structured, object oriented and functional programming.

It is **dynamically typed** and **garbage-collected** and offers a comprehensive standard library.

## Basics

In Python, expressions are made up of values and operators. They always evaluate down to a single value. Every value belongs to one data type.

In a Python script, we can wait for user input by using ```input()```.

The ```str()``` and ```int()``` functions return a string/int. ```float()``` returns a float value.

For example:
```python
print('I am printing ' + str(int(numberVariable) + 1))    

#int() takes the content of numberVariable as an int
#str() turns it all into a string
```

We can add comments using ```#```.

## Strings

In Python, strings are defined by using ```' '``` single quotes. Strings can be concatenated by using a ```+``` and replicated using a ```*```.

```python
'Alice' + 'Bob'       #This will return 'AliceBob'
```

```python
'Alice' * 3       #This will return 'AliceAliceAlice'
```

If we want to get the length of a string, we can use the ```len(myString)```function.

## Flow control

### Boolean

Two values: ```True``` & ```False``` (they need to be typed with a capital T or F)

When we set a variable based on ```input()``` a **blank string** would return false, all the other strings return true. For numbers, **0** or **0.0** return false, all others return true. ```bool(0)``` would return false.

#### Boolean operators

Check truth table. AND, OR, NOT...

### Comparison operators

They evaluate to a boolean value. 

```python
 ==
 !=
 <
 >
 <=
 >=
```

Integers and strings are always **not equal** to each other. Float values and integer values **can** be equal to each other.

### If - else - elif

```python
name = 'Alice'
if name == 'Alice':
  print('Hi Alice')
print('Done')
```

If the condition is true, the indented code is executed, otherwise the non indendet code is executed.

New blocks (part with new intendation) begin only after statements that end with a colon like in the IF statement.

```python
password = 'swordfish'
if password == 'swordfish':
  print('Access granted.')
else:
  print('Wrong password.')
```

**Elif** can follow an if statement. It lets us check for multiple conditions. As soon as one condition is met, all the other if statements are **skipped**. This means the order of the conditions **matter**.

```python
name = 'Bob'
age = 3000
if name = 'Alice':
  print('Hi Alice')
elif age < 12:
  print('You are not Alice, kiddo.')
```

### While loops

```python
test = 1
while test < 5:
  print('Hello world!')
  test = test + 1
```

```python
name = ''
while name != 'matko':
  print('Please type your name.')
  name = input()
print('Thank you')
```

```break``` causes our execution jump out of the loop.

```continue``` jumps back to the start of the loop and reevaluates our loop's condition.

### For loops

Loops a specific number of times.

```python
for i in range(5):
  print('Number of times this has been printed: ' + str(i+1))
```

Another example that adds all the numbers from 0 to 100.

```python
total = 0
for num in range(101):
  total = total + num
print(total)
```

We can also use ```break``` and ```continue``` statements in for loops.

#### Range

The ```range()``` function returns a value of type ```range```. ```range(10)``` gives us a range from 0 to 9.

```range(12,16)``` starts at 12 and goes up to, but not including 16.

We can also call the range function with 3 arguments: the first is the start, the second the end, and the third is a ```step``` argument. The ```step``` argument is the amount that the variable is increased (or decreased if the argument is negative) after each iteration. 