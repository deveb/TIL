# Lecture 1: C

Notes: [https://cs50.harvard.edu/x/2020/notes/1/](https://cs50.harvard.edu/x/2020/notes/1/)

## Lecture

                           ┌━━━━┐  
source code →│compiler│→ machine code  
                           └────┘ 

```bash
$ clang hello.c
$ ./a.out
```

$: prompt

UNIX/Linux command 

ls, rm, mkdir, rm dir

```bash
$ clang -o string string.c -lcs50
$ make string
```

* * Conditions - if-else
* Loops - while, for
* Data types - bool, char, double, float, int, long, string
* Logical - \|\|, &&

디자인에 대한 이야기

1. 같은 코드 세번 복붙
2. 같은 코드 함수화 + for loop

마리오 코드

RAM: finite Hardware

1. 1/10 이 왜 0.1000000000 이 아닌가? finite amount information 을 저장하기 때문에 근사치를 저장한다.
2. 3자리수 999에 1을 더하면? 000
3. Y2K 문제
4. 787 보잉

## Shorts

### Data Types

* int: 4bytes\(32bits\). -2^31 ~ 2^31-1
  * unsigned int: 0 ~ 2^32-1
* char: 1byte
* float: 4bytes
* double: 8bytes
* void: type but dot data type. returns nothing

cs50 supports

* bool
* string

declaration &gt; assignment == initialization

### Operators

Arithmetic Operators: add, subtract, multiply, divide, modulus, \*=, ++

Boolean expressions: true\(except zero\) or false\(zero\)

* Logical operators: AND\(&&\), OR\(\|\|\), NOT\(!\)
* Relational operators: &lt;, &lt;=, &gt; &gt;=, == !=

### Conditional Statements

if\(boolean-expression\) { }

if\(boolean-expression\) { } else { }

if\(boolean-expression\) { } else if\(boolean-expression\)  { } else { }

switch \(condition\) { case 1: break; case 2: break; default: }

\(expr\) ? true : false

### Loops

while \(boolean-experession\) { }

do { } while \(boolean-expression\)

for\(start; expr; increment\) { }

### Command Line

cs50 sandbox is Ubuntu.

Linux commands

* ls: list
* cd: change directory
* pwd: presence working directory
* ctrl + l: clears screen
* mkdir: make dir
* cp \[-r\] &lt;source&gt; &lt;target&gt;: copy
* rm \[-rf\]: remove
* mv: move 





