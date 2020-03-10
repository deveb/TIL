# week 2

## III. DIVIDE & CONQUER ALGORITHMS

### O\(n log n\) Algorithm for Counting Inversions I

One way to solve collaborative filtering

```text
pictorially: 그림
```

### O\(n log n\) Algorithm for Counting Inversions II

### Strassen's Subcubic Matrix Multiplication Algorithm

Non trivial. Multiplying two matrices

### O\(n log n\) Algorithm for Closest Pair I \[Advanced - Optional\]

### 'O\(n log n\) Algorithm for Closest Pair II \[Advanced - Optional\]

## IV. THE MASTER METHOD

### Motivation

A general mathematical tool for analyzing the running time of divide and conquer algorithms.

```text
truism: 자명한 이
quadratic: N^2
cubic: N^3
```

#### **2 ingredients of recurrence**

* base case, describing the running time when there's no further recursion.
  * 
* generel case, when you're not in the base case, and you make recursive calls.

#### **The running time in terms of 2 pieces**

* The work done by the recursive calls
* The work done outside of the recursive calls.

#### **A Recursive Algorithm**

* T\(n\) = Maximum number of operations, this algorithm needs to multiply two n-digit numbers.
* Recurrence: express T\(n\) in terms of running time of recursive calls
* Base case: T\(1\) &lt;= a constant
* For all n &gt; 1 : T\(b\) &lt;= 4T\(n/2\) + O\(n\)
  * 4T\(n/2\): Work done by recursive calls
  * O\(n\): work done here

### Formal Statement

#### Recurrence format

* Base case: T\(n\) &lt;= a constant for all sufficiently small n.
* For all larger n: T\(n\) &lt;= aT\(n/b\) + O\(n^d\)
  * a= number of recursive calls\(&gt;=1\)
  * b = input size shrinkage factor\(&gt;1\)
  * d= exponent in running time of work done outside of recursive calls \(&gt;=0\)
  * a, b,. d indenpendent of n

### **The Master Method**

![](../../../../.gitbook/assets/image%20%287%29.png)

1. the runing time is the same as the running time in the recurrence outside of the recursive call, but pick up an extra log N factor. logarithm base doesn't matter.
2. a is smaller than b to the d: dominated by what's done outside the recursion in the outermost call.
3. a is strictly bigger than b.logarithm base does matter.

### Proof 1

![](../../../../.gitbook/assets/image%20%2813%29.png)

![](../../../../.gitbook/assets/image%20%289%29.png)

![](../../../../.gitbook/assets/image%20%281%29.png)

