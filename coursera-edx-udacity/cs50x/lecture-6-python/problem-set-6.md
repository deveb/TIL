# Problem set 6

```python
import sys


def main(csv, text):
    pattern = []
    database = {}
    with open(csv, 'r') as file:
        for line in file:
            line = line.rstrip('\n')
            if not pattern:
                pattern = line.split(',')[1:]
            else:
                data = line.split(',')
                database[data[0]] = [int(r) for r in data[1:]]
    
    sequence = None
    with open(text, 'r') as file:
        for line in file:
            line = line.rstrip('\n')
            sequence = line
    
    # print(sequence)
    for name, repeat in database.items():
        is_valid = True
        for i, r in enumerate(repeat):
            if pattern[i] * r not in sequence or pattern[i] * (r + 1) in sequence:
                is_valid = False
                break
        if is_valid:
            print(name)
            return

    print("No match")
    return
    

if __name__ == '__main__':
    try:
        main(sys.argv[1], sys.argv[2])
    except IndexError:
        print("Usage: python dna.py data.csv sequence.txt")
```

