# Problem set 2

```c
#include <stdio.h>
#include <cs50.h>
#include <string.h>
#include <math.h>

int main(void)
{
    string text = get_string("Text: ");
    int letters = 0;
    int sentences = 0;
    int words = 0;

    char *pointer = strtok(text, " ");
    while (pointer != NULL)
    {
        for (int i = 0; i < strlen(pointer); i++)
        {
            if ((pointer[i] >= 'a' && pointer[i] <= 'z') || (pointer[i] >= 'A' && pointer[i] <= 'Z'))
            {
                letters++;
            }
            else if (pointer[i] == '.' || pointer[i] == '?' || pointer[i] == '!')
            {
                sentences++;
            }
            else if (pointer[i] == '\'' && pointer[i + 1] != 's')
            {
                words++;
            }
        }
        words++;
        pointer = strtok(NULL, " ");
    }
    // printf("%i letters, %i sentences, and %i words.\n", letters, sentences, words);

    // L is the average number of letters per 100 words in the text
    // S is the average number of sentences per 100 words in the text.
    // index = 0.0588 * L - 0.296 * S - 15.8
    float index = 0.0588 * (letters * 100 / words) - 0.296 * (sentences * 100 / words) - 15.8;
    index = round(index);

    if (index > 16)
    {
        printf("Grade 16+\n");
    }
    else if (index < 1)
    {
        printf("Before Grade 1\n");
    }
    else
    {
        printf("Grade %d\n", (int)index);
    }
}
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <cs50.h>

bool validate(char *argv[]);

int main(int argc, char *argv[])
{
    if (!validate(argv)) {
        printf("Usage: ./caesar key\n");
        return 1;
    }
    int key = atoi(argv[1]);
    string text = get_string("plaintext: ");
    printf("ciphertext: ");
    for (int i = 0; i < strlen(text); i++)
    {
        if (text[i] >= 'a' && text[i] <= 'z')
        {
            printf("%c", 'a' + (text[i] - 'a' + key) % 26);
        }
        else if (text[i] >= 'A' && text[i] <= 'Z')
        {
            printf("%c", 'A' + (text[i] - 'A' + key) % 26);
        }
        else
        {
            printf("%c", text[i]);
        }
    }
    printf("\n");
}

bool validate(char *argv[])
{
    if (argv[1] == NULL || argv[2] != NULL)
    {
        return false;
    }
    for (int i = 0; i < strlen(argv[1]); i++)
    {
        if (argv[1][i] < '0' || argv[1][i] > '9')
        {
            return false;
        }
    }
    return true;
}
```

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <cs50.h>

bool validate(char *key);

int main(int argc, char *argv[])
{
    if (argv[1] == NULL || argv[2] != NULL)
    {
        printf("Usage: ./substitution ke\ny");
        return 1;
    }
    if (!validate(argv[1])) {
        printf("Key must contain 26 characters.\n");
        return 1;
    }
    string key = argv[1];
    string text = get_string("plaintext: ");
    printf("ciphertext: ");
    for (int i = 0; i < strlen(text); i++)
    {
        if (text[i] >= 'a' && text[i] <= 'z')
        {
            printf("%c", tolower(key[(text[i] - 'a') % 26]));
        }
        else if (text[i] >= 'A' && text[i] <= 'Z')
        {
            printf("%c", toupper(key[(text[i] - 'A') % 26]));
        }
        else
        {
            printf("%c", text[i]);
        }
    }
    printf("\n");
}

bool validate(char *key)
{
    int index[26] = {0};
    for (int i = 0; i < strlen(key); i++)
    {
        if ((key[i] >= 'a' && key[i] <= 'z') || (key[i] >= 'A' && key[i] <= 'Z'))
        {
            index[tolower(key[i]) - 'a']++;
        }
    }
    for (int i = 0; i < 26 ; i++)
    {
        if (index[i] != 1)
        {
            return false;
        }
    }
    return true;
}

```

