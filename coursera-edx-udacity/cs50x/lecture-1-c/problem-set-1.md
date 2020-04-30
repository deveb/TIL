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

```c
#include <cs50.h>
#include <stdio.h>
#include <math.h>

int main(void)
{
    int quarter = 25;
    int dime = 10;
    int nickel = 5;
    int penny = 1;
    int coin = 0;
    int count = 0;
    do
    {
        float dollar = get_float("Change owed: ");
        coin = round(dollar * 100);
    }
    while (coin < 0);

    while (coin >= quarter)
    {
        count++;
        coin -= quarter;
    }
    while (coin >= dime)
    {
        count++;
        coin -= dime;
    }
    while (coin >= nickel)
    {
        count++;
        coin -= nickel;
    }
    
    while (coin >= penny)
    {
        count++;
        coin -= penny;
    }

    printf("%d\n", count);
}

```

```c
#include <cs50.h>
#include <stdio.h>
#include <math.h>

int main(void)
{
    int count = 0;
    int checksum = 0;
    long card_numbers = 0;
    do
    {
        card_numbers = get_long("Number: ");
    }
    while (card_numbers < 0);

    long digit = card_numbers;
    while (digit)
    {
        if (count % 2 == 1)
        {
            int products_digit = digit % 10 * 2;
            while (products_digit)
            {
                checksum += products_digit % 10;
                products_digit = products_digit / 10;
            }
        }
        else
        {
            checksum += digit % 10;
        }
        digit = digit / 10;
        count ++;
    }

    if (checksum % 10 != 0)
    {
        printf("INVALID\n");
    }
    else
    {
        if (card_numbers / 1000000000000000 == 4
            || card_numbers / 100000000000000 == 4
            || card_numbers / 10000000000000 == 4
            || card_numbers / 1000000000000 == 4)
        {
            printf("VISA\n");
        }
        else if (card_numbers / 10000000000000 == 34
                 || card_numbers / 10000000000000 == 37)
        {
            printf("AMEX\n");

        }
        else if (card_numbers / 100000000000000 == 51
                 || card_numbers / 100000000000000 == 52
                 || card_numbers / 100000000000000 == 53
                 || card_numbers / 100000000000000 == 54
                 || card_numbers / 100000000000000 == 55)
        {
            printf("MASTERCARD\n");
        }
        else
        {
            printf("INVALID\n");
        }
    }
}

```

