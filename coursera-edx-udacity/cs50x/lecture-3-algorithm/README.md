# Lecture 3: Algorithm

Linear search, O\(n\)  
Binary Search, O\(logn\)

Big O : Worst case  
Omega Ω : best case  
Theta θ : Meet both

* O\(n^2\)        Bubble sort, Selection sort 
* O\(n log n\)  Merge sort
* O\(n\)            Linear search
* O\(log n\)      Binary search
* O\(1\)



* Ω \(n^2\)        Selection sort 
* Ω \(n log n\)  Merge sort
* Ω \(n\)            Bubble sort
* Ω \(log n\)      
* Ω \(1\)             Linear search, Binary search



* θ \(n^2\)        Selection sort 
* θ \(n log n\)  Merge sort

```text
typedef struct 
{
    string name;
    string number;
}
person;

...

person people[4];
people[0].name;
people[0].number;
```

Recursive call  
base case

## Linear Search

Iterate across the array from left to right, searching for specified element.

Worst: O\(n\), Best: Ω \(1\)

## Binary Search

divide and conquer, reducing serarch area by half each time, trying to find a target number.

Array must be sorted

Worst: O\(log n\), Best: Ω \(1\)

## Bubble Sort

Move highrt valued elements generally towards the right and lower value elements generally towards left.

Worst: O\(n^2\), Best: Ω \(n\)

## Selection Sort

Find the smallest unsorted element and add it to the end of the sorted list.

Worst: O\(n^2\), Best: Ω \(n^2\)

## Insertion Sort

Build your sorted array in place, shifting elements out of the way if necessary to make room as you go

Worst: O\(n^2\), Best: Ω \(n\)

## Recursion

call itself

factorial function \(n!\)  
fibonacci - multiple base case  
The collatz conjecture - multiple recursive case

base case: terminate the recursive process  
recursive case

In general, recursive functions replace loops in non-recursive functions.

## Merge Sort

Sort smaller arrays and then combine those arrays together in sorted order

Worst: O\(nlogn\), Best: Ω \(nlogn\)

## Algorithm Summary

![](../../../.gitbook/assets/image%20%2818%29.png)

