# Sort

### 42746

```python
# did not passed
def solution(numbers):
    strings = [str(n) for n in numbers]
    def _sort(s):
        slen = len(s)
        if slen == 1:
            return s.ljust(4,s)
        elif slen == 2:
            return s + s
        elif slen == 3:
            return s.ljust(4, s [-1])
        else:
            return s
    answer = sorted(strings, key=_sort, reverse=True)
    return str(int(''.join([str(a) for a in answer])))
```

### 42747

```python
def solution(citations):
    citations = sorted(citations, reverse=True)
    count = 0
    for c in citations:
        if count >= c:
            return count
        count += 1
    return count
```

### 42748

```python
def solution(array, commands):
    answer = []
    for start, end, nth in commands:
        answer.append(sorted(array[start-1:end])[nth-1])
    return answer
```

