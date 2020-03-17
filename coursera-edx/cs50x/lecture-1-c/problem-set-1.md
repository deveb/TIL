---
description: 'https://cs50.harvard.edu/x/2020/psets/1/'
---

# Problem set 1

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int n = 0;
    do
    {
        n = get_int("Height: ");
    }
    while (n <= 0 || n >= 9);

    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            printf(" ");
        }
        for (int j = 0; j < i + 1; j++)
        {
            printf("#");
        }
        printf("\n");
    }
}
```

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int n = 0;
    do
    {
        n = get_int("Height: ");
    }
    while (n <= 0 || n >= 9);

    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            printf(" ");
        }
        for (int j = 0; j < (i + 1) * 2 + 2; j++)
        {
            if (j == (i + 1) || j == (i + 2))
            {
                printf(" ");
            }
            else
            {
                printf("#");
            }
        }
        printf("\n");
    }
}

```

