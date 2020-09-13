# 2018 WinterCoding

## 스킬 트리

```python
def solution(skill, skill_trees):
    answer = 0
    intersect = []
    for st in skill_trees:
        intersect.append(''.join([s for s in st if s in skill]))
    
    correct = [skill[:i + 1] for i in range(len(skill))]
    for i in intersect:
        if i in correct or not i:
            answer += 1
    return answer
```

## 방문 길이

```python
def solution(dirs):
    position = [0, 0] # X, Y
    visited = {}
    answer = 0
    for d in dirs:
        prev_position = position.copy()
        if d == 'U' and position[0] > -5:
            position[0] -= 1
        elif d == 'D' and position[0] < 5:
            position[0] += 1
        elif d == 'L' and position[1] > -5:
            position[1] -= 1
        elif d == 'R' and position[1] < 5:
            position[1] += 1
        if prev_position  == position:
            continue
        if tuple(prev_position + position) not in visited:
            answer += 1
            visited[tuple(prev_position + position)] = True
            visited[tuple(position + prev_position)] = True
        print(tuple(prev_position + position))
    return answer
```

## 쿠키 구입

```python
def solution(cookie):
    answer = 0
    size = len(cookie)
    sums =  [[0 for col in range(size)] for row in range(size)]
    for i in range(size):
        for j in range(size - i):
            if j == j + i:
                sums[j][j + i] = cookie[j]
            else:
                # sums[j][j + i] = sum(cookie[j: j+i + 1])
                sums[j][j + i] = sums[j][j + i -1] + sums[j + 1][j + i] - sums[j + 1][j + i -1]
    for i in range(size):
        for j in range(i, size - 1):
            if sums[i][j] < answer:
                continue;
            if sums[i][j] > sums[j + 1][size -1]:
                break;
            for k in range(j + 1, size):
                # print((i,j), (j + 1, k))
                if sums[i][j] == sums[j + 1][k]:
                    answer = max([answer,sums[i][j]])
    return answer
```

