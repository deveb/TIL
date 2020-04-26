# Lecture 4: Memory

Hexadecimal 

`printf("%p\n", &n);` What's the address

`printf("%i\n", *&n);` Go to the address

There is no string

```c
char *s = "EMMA";
printf("%s\n", s);
printf("%p\n", s);
printf("%p\n", &s[0]);
printf("%p\n", &s[1]);
printf("%p\n", &s[2]);
printf("%p\n", &s[3]);
```

syntactic sugar: handy features

```c
char *s = "EMMA";
printf("%c\n", *s);
printf("%c\n", *(s+1));
printf("%c\n", *(s+2));
printf("%c\n", *(s+3));
```

String copy

```c
char *s = get_string("s: ");
char *t = malloc(stren(s) + 1);

for(int i = 0, n = strlen(s); i < n + 1; i++)
{
    t[i] = s[i];
}
```

`strcpy(t, s);`

malloc ↔ free  
valgrind

Swap  
pass by reference

```c
void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```

```c
char s[5];
printf("s: ");
scanf("%s", s);
printf("s: %s\n", s);
```

## Hexadecimal

base-16  
0 1 2 3 4 5 6 7 8 9 A B C D E F

## Pointers

Alternative way to pass data between functions.

Disk drives are just storage space. Manipulation and use of data can only take place in RAM.

Random Access Memory

![](../../.gitbook/assets/image%20%288%29.png)

Pointers are just addresses  
value is a memory address  
type describes the data located at that memory address

dereferencing `int* p`

## Dynamic Memory Allocation

Dynamically allocated memory comes from a pool of memory known as the heap

All memory we've been working with has been coming from a pool of memory known as the stack

![](../../.gitbook/assets/image%20%285%29.png)

`malloc()`

Dynamically-allocated memory is not automatically returned to the system for later use.

![](../../.gitbook/assets/image%20%2821%29.png)

![](../../.gitbook/assets/image%20%2823%29.png)

`free()`



## Call Stacks

When you call a function, the system sets aside space in memory for that function to do its necessary work  
Frequently call such chunks of memory stack frames or function frames

These frames are arranged in a stack  
When a new function is called, a new frame is pushed on to the top of the stack and becomes the active frame.  
When a function finishes its work, its frame is popped off of the stack, and the frame immediately below it becomes the new active function on the top of the stack.

factorial

![](../../.gitbook/assets/image%20%2830%29.png)

## File Pointers

`FILE*`, `fopen()`, `fclose()`, `fgetc()`, `fputc()`, `fread()`, `fwrite()`

![](../../.gitbook/assets/image%20%2833%29.png)

