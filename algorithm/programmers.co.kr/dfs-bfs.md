# DFS/BFS

### 43162

```python
def solution(n, computers):
    def bfs(start):
        queue = [start]
        visited = []
        while queue:
            popped = queue.pop(0)
            for index, node in enumerate(computers[popped]):
                if not node:
                    continue
                if index not in visited:
                    visited.append(index)
                    queue.append(index)
        return visited
        
    paths = []
    starts = [s for s in range(n)]
    while starts:
        visited = bfs(starts[0])
        starts = list(set(starts) - set(visited))
        paths.append(visited)
    return len(paths)
```

### 43163

```python
def solution(begin, target, words):
    step = len(begin)
    
    queue = [(begin, [begin])]
    while queue:
        node, path = queue.pop(0)
        if node == target:
            return len(path) -1
        for w in words:
            if w in path:
                continue
            if len(set(node) - set(w)) == 1:
                queue.append((w, path + [w]))
    
    return 0
```

### 43165

```python
def solution(numbers, target):
    def _calc(array=[]):
        if len(numbers) == len(array):
            if sum(array) == target:
                return 1
            return 0
        else:
            number = numbers[len(array)]
            return _calc(array + [number]) + _calc(array + [-number])
    
    return _calc()
```

