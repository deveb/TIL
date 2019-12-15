# Divide and Conquer, Sorting and Searching, and Randomized Algorithms

## week 1, Divide and Conquer, Sorting and Searching, and Randomized Algorithms

### I. INTRODUCTION

#### Integer Multiplication

Well defined set of rules for transforming input into an output for solving a computational problem

**Lecture pattern**

1. Define a computational problem
2. input, desired output
3. solution, algorithm that transforms the input to the output

```text
digression: 본문을 벗어나 여담
quadratic: 이차의
obedient tumidity 
succinctly 간결하게
apropos 에 관하여
```

#### Karatsuba Multiplication

Recursive algorithms need a base case.

```text
gloss over: 얼버무리고 넘어가다
bonafide: 진실된, 진짜의
per se: 그 자체가
ingenuity: 독창성
bear fruit: 결실을 보다
```

#### About the Course

Big-Oh notation: A modeling choice about the granularity with which we measure a performance metric.

```text
canonical: 표준이 되는
logarithm: 로그
regurgitate: (삼킨 음식물을 입 안으로 다시) 역류시키다, (듣거나 읽은 내용을 별 생각 없이) 
regale: 융숭하게 대접하다. 매우 즐겁게 해주다.
```

#### Merge Sort: Motivation and Example

Divide-and-Conquer, break down the problem into smaller sub problems which solve recursively, and then combine the results of the smaller sub-problem to get a solution to the original problem.

```text
asymptotic: 점근선의
```

#### Merge Sort: Pseudocode

Base case, when the input is sufficient, you don't do any recursion, you just return some trivial answer Running time is similar with the number of lines of code excuted log N, Number of times you divide by 2 until you get down to 1.

```text
transcend: 초월하다
bog down: 교착 상태에 빠지다. 늪에 가라앉히다.
crude: 대충의, 대강의
```

#### Merge Sort: Analysis

```text
substantiate: 입증하다 facilitate: 가능하게 하다.
```

#### Guiding Principles for Analysis of Algorithms

**3 Assumptions**

1. Worst-case analysis
2. Won't pay much attention to constant factors, lower-order terms

   Understanging tiny constant factors in the analysis is an inappropriate level of granularity.

3. asymptotic analysis

Fast algorithm ≈ Worst-case running time grows slowly with input size

```text
tractability: 다루기 쉬운 unduly: 과도하게 cavalierly: 무신경한, 거만한
```

### II. ASYMPTOTIC ANALYSIS

#### The Gist

High level discussion to Mathmatical formalism

```text
gist: 요지 segue: 넘어가다 coarse: 거친, 굵은
```

#### Big-Oh Notation

#### Basic Examples

#### Big Omega and Theta

```text
ubiquitous 어디에나 있는, 아주 흔한
```

## week 2, Divide and Conquer, Sorting and Searching, and Randomized Algorithms

### III. DIVIDE & CONQUER ALGORITHMS

#### O\(n log n\) Algorithm for Counting Inversions I

#### O\(n log n\) Algorithm for Counting Inversions II

#### Strassen's Subcubic Matrix Multiplication Algorithm

#### O\(n log n\) Algorithm for Closest Pair I \[Advanced - Optional\]

#### 'O\(n log n\) Algorithm for Closest Pair II \[Advanced - Optional\]

### IV. THE MASTER METHOD

#### Motivation

**2 infredients of recurrence**

* base case, describing the running time when there's no further recursion.
* generel case, when you're not in the base case, and you make recursive calls

**The running time in terms of 2 pieces**

* The work done by the recursive calls
* The work done outside of the recursive calls.

#### Formal Statement



