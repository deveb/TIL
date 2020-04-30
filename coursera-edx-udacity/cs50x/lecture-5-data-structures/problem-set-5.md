# Problem set 5

```c
// Implements a dictionary's functionality

#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>


#include "dictionary.h"

// Represents a node in a hash table
typedef struct node
{
    char word[LENGTH + 1];
    struct node *next;
}
node;

// Number of buckets in hash table
const unsigned int N = 2048;

// Hash table
node *table[N];

// Returns true if word is in dictionary else false
bool check(const char *word)
{
    char lowercase[LENGTH + 1] = {};
    for (int i = 0; word[i]; i++)
    {
        lowercase[i] = tolower(word[i]);
    }
    int key = hash(lowercase);

    node *t = NULL;
    t = table[key];
    while (t != NULL)
    {
        if (strcmp(t->word, lowercase) == 0)
        {
            return true;
        }
        t = t->next;
    };
    return false;
}

// Hashes word to a number
unsigned int hash(const char *word)
{
    int sum = 0;
    for (int i = 0; word[i] != '\0'; i++)
    {
        sum += word[i];
    }

    return sum % N;
}

// Loads dictionary into memory, returning true if successful else false
bool load(const char *dictionary)
{
    FILE *file = fopen(dictionary, "r");

    if (file == NULL)
    {
        return false;
    }
    char word[LENGTH + 1], ch;
    int index = 0;

    // Spell-check each word in text
    for (int c = fgetc(file); c != EOF; c = fgetc(file))
    {
        // Allow except line break
        if (c != '\n')
        {
            // Append character to word
            word[index] = c;
            index++;

            // Ignore alphabetical strings too long to be words
            if (index > LENGTH)
            {
                // Consume remainder of alphabetical string
                while ((c = fgetc(file)) != EOF);

                // Prepare for new word
                index = 0;
            }
        }
        // We must have found a whole word
        else if (c == '\n' && index > 0)
        {
            // Terminate current word
            word[index] = '\0';
            index = 0;

            // Update counter

            int key = hash(word);
            if (table[key] == NULL)
            {
                table[key] = malloc(sizeof(node));
                strcpy(table[key]->word, word);
                table[key]->next = NULL;
            }
            else
            {
                node *t = NULL;
                t = table[key];
                while (t->next != NULL)
                {
                    t = t->next;
                };
                node *n = malloc(sizeof(node));
                strcpy(n->word, word);
                n->next = NULL;
                t->next = n;
            }
        }
    }

    fclose(file);
    return true;
}

// Returns number of words in dictionary if loaded else 0 if not yet loaded
unsigned int size(void)
{
    unsigned int count = 0;
    for (int i = 0; i < N; i++)
    {
        node *t = NULL;
        t = table[i];
        while (t != NULL)
        {
            count++;
            t = t->next;
        };
    }
    return count;
}


// Unloads dictionary from memory, returning true if successful else false
bool unload(void)
{
    for (int i = 0; i < N; i++)
    {
        while (table[i] != NULL)
        {
            node *tmp = table[i]->next;
            free(table[i]);
            table[i] = tmp;
        }
    }
    return true;
}

```

