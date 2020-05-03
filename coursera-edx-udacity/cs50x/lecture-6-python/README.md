# Lecture 6: Python

* range: sequence of numbers
* list: sequence of mutable values
* tuple: sequence of immutable values
* dict: collection of key/value pairs
* set: collection of unique values

Regular expressions

* yes\|y
* y\(es\)?
* ^y\(es\)?
* ^y\(es\)?$

## Python

Variables: no type specifier. Declared by initialization only.  No semicolon.

Conditionals: Use or, and instead \|\|, &&. Use colon instead curly bracket.  
ternary operator: True if True else False

Loops: while and for.

Arrays: known as lists. not fixed in size. splice with colon.

Tuples: ordered, immutable sets of data.

Dictionaries: order not guaranteed  
for key in dict:  
for key, cal in dict.items\(\):

Functions: def keyword. no need for main

Objects: python is OOP, c has struct. Use class keyword. requires initialization function as known as a constructor. each method of object self is the first parameter.

Method: function inside object  
function\(\)  
object.method\(\)

```python
class Student():

    def __init__(self, name, id):
        self.name = name
        self.id = id

    def changeID(self, id):
        self.id = id

    def print(self):
        print("{} - {}".format(self.name, self.id))  

```

Style: good style is crucial in python. tabs and indentation actually matter in language.

Including:  
import something  
something.other\(\)

Run: python &lt;file&gt;













