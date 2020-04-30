# Lecture 5: Data Structures

\(\*n\).number  
n-&gt;number

Queue\(FIFO\)

enqueue  
dequeue

Stack\(LIFO\)

pop  
push

dictionary = hash table

## Data Structures

Arrays

* Insertion is bad
* Deletion is bad
* Lookup is great - constant time
* Relatively easy to sort
* Relarively small size-wise
* Fixed size, no flexibility

Linked lists

* Insertion is easy
* Deletion is easy
* Lookup is bad - linear search
* Reletively difficult to sort
* Relatively small size-wise

Hash tables

* Insertion is a two-step process - hash and add
* Deletion is easy
* Lookup is on average better than linked lists
* Not an ideal data structure for sorting
* Can run the gamut of size

Tries

* Insertion is complex
* Deletion is easy
* Lookup is fast
* Already sorted
* Rapidly becomes huge, not great for space 

## Singly-Linked Lists

```c
typedef struct sllist
{
    VALUE val;
    struct sllist *next;
}
sllnode;
```

operations

1. create
   1. dynamically allocate space. make sure didn't run out of memmory
   2. initialize val and next
   3. return a pointer to the newly created sllnode
2. search
   1. create traversal pointer pointing to the list's head
   2. check current node's val
   3. set the traversal pointer to the next pointer and go back to step b
3. insert
   1. Dynamically allocate space for a new sllnode. make sure didn't run oom
   2. populate and insert the node at the beginning of the linked list
   3. return a pointer to the new head of the linked list
4. destory
   1. If you'be reached a null pointer, stop/
   2. Delete the rest of the list.
   3. Free the current node

## Hash Tables

Hash tables combine the random access ability of an array with the dynamism of a linked list

* Insertion can start to tend toward θ\(1\)
* Deletion can start to tend toward θ\(1\)
* Lookup can start to tend toward θ\(1\)

1. Hash function: which returns an nonnegative integer value called a hash code
2. Array: capable of sorting data of the type we wish to place into the data structure

A good hash function should:

* Use only the data being hashed
* Use all of the data being hashed
* Be dereministic
* Uniformly distribute data
* Generate very different hash codes for very similar data

Collision

occurs when two pieces of data, when run through the hash function, yield the same hash code.

Resolving collision: Linear probing  
Linear probing is subject to a broblem called clusterring. Once there's a miss, two adjacent cells will contain data, making it more likely in the future that the cluster will go

Resolving collision: Chaining  
Pull it all together.  
For lookup, could be one huge list across n lists

## Tries

combine structures and pointers together to store data

search: If you can follow the map from beginning to end then data exists.





{% embed url="https://www.bigocheatsheet.com/" %}



