# Sorting algorithms

The **Big O notation** describes how slow an algorithm becomes once the complexity of the inputs rises. For example `O(n²)` -> the execution times rises to the square in relation to the amount of inputs.

The lowest possible Big O notation is -> `O(1)`.

`O(n)` means the complexity rises in a constant/linear way.

## Bubble sort

* pair-wise swapping -> values next to each other are compared and if necessary swapped
* this is is repeated until no swappings occur anymore
* not very efficient because the the we always have to go through all elements in the list -> **O(n²)**

## Quick sort

* "divide and conquer"
* two partial lists created using the pivot element (one list with all values smaller than the pivot element and the other with the values that are larger, values equal to the pivot can be added to either)
* Then the quick sort algorithm is applied again to the partial lists with a new pivot element, this is repeated until each partial list has a length of 0 or 1
* Worst case -> **O(n²)**, but usually it is faster than that

## Merge sort

* list divided into smaller lists until each list only contains one element (a list of one element is considered sorted)
* the sublists are then repeatedly merged to produce new sorted sublists until there is only one sublist remaining

## Selection sort

* There is a sorted list S and an unsorted list U, at the beginning S is empty and U contains all values
* We look for the smallest element in U and swap it with the first element in U
* The smallest element is moved to the sorted list S
* This is repeated until U is empty

## Insertion sort

* We iterate from the first element to the last element in the list
* If the current element is smaller than its predecessor, we move it one position up and compare it again the **new** predecessor - if necessary we move it up again
* Then the next element is again compared with the element before it and 
* Each element is moved closer and closer to the beginning of the list
* Not very efficient but runs **in place** (O(n²)), usually faster than bubble sort