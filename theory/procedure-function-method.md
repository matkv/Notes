# Procedures, functions & methods

Procedures and functions are small sections of code that are used to perform a particular task. They are used to avoid repition of commands within the program.

## Procedure

The main difference between a procedure and a function is that procedures **don't** return a value.

## Function

Sub-program that **returns** a value. They can be used directly in statements.

### Call by value

Parameters are used with their **value**. Inside of the function we are working with a **copy** of the values and changes to the values of the parameters **do not** affect the actual original values.

Example in C#:

```csharp
public void swapContent(int a, int b)
{
    int temp = a;
    a = b;
    b = temp;

    //a & b have only changed locally
}
```

### Call by reference

When using call by reference, changes to the parameters inside the function **affect the original values outside of it**.

```csharp
public void swapContent(ref int a, ref int b)
{
    int temp = a;
    a = b;
    b = temp;

    //a and be have also changed outside the function
}
```

## Method

Methods are used in object oriented programming and describe the behavior of objects. A method is the function/procedure of an object.

Objects can be "connected" with others using methods.
