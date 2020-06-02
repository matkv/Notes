# Variable

* Symbolic representation of the storage adress of data - associated with a name
* Contains a value
* Described by the type
* The value can, in contrast to a constant, be changed during runtime
* `data type` + `name`

When using variables, for example in functions, we differentiate between **calling by value** and **calling by reference** (values & references/pointers).

* Call by value - the value of the variable is used, changes to the variable **don't** change the original variable
* Call by reference - the **reference** to the original variable is used, the same storage adress is used. Changes to the variable **change the original variable**.

## Declaring variables

* **Static typing** - the type is bound to the *variable*. Types are checked at **compile time**.
* **Dynamic typing** - the type is bound to the *value*. Types are checked at **run time**.


* **Implicit declaration** - the type is not specified when declaring the variable but is inferred by the value
* **Weak typing** - the compiler does not enforce a typing discipline. For example `x = "1.5"` (a string) - `x*2` returns 3 anyways. The compiler doesn't throw an error but converts the string to a number. Weak typing can lead to errors more easily, but it also generally makes writing the code easier.
