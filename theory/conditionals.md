# Conditionals

* Selection - choosing between or multiple outcomes
    * Selection - one choice -> **if**
    * Selection - two choices -> **if-else**
    * Selection - multiple choices -> **if-elseif-else** or **switch-case**
* Iteration - repetition/looping as long as a condition is met
    * count-controlled loops -> **for-loop**
    * condition-controlled loops -> **while-loop** & **do-while**
    * collection-controlled loops -> **foreach loop**

We differentiate between a loop where the condition is checked before running it for the first time and vice-versa:

```
WHILE condition DO loop-body        //(kopfgesteuert)

DO loop-body WHILE condition        //(fußgesteuert)
REPEAT loop-body UNTIL condition    //(fußgesteuert)
```

## Termination conditions

When working with loops, the **termination condition** decides when a loop will stop.

For example in a **while-loop** we usually have the **break** and **continue** statements:

* break - exit the loop, continue with normal program flow
* continue - exit the current iteration of the loop and start again from the start of the loop

## Recursion

Procedure/ function which calls itself. Here the termination condition is also important.