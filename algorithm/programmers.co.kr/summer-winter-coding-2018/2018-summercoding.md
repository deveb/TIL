# 2018 SummerCoding

## 예산

```python
def solution(d, budget):
    d.sort()
    sum = 0
    for i in range(len(d)):
        sum += d[i]
        if sum > budget:
            return i
    return i + 1
```

## 영어 끝말잇기

```python
def solution(n, words):
    visited = {words[0]: True}
    for i in range(1, len(words)):
        if words[i] in visited or words[i - 1][-1] != words[i][0]:
            return i % n + 1, i // n + 1
        visited[words[i]] = True
    return [0, 0]
```

## 숫자게임

```python
def solution(A, B):
    answer = 0
    A.sort()
    B.sort()
    for a in A:
        for b in B:
            if a < b:
                B.remove(b)
                answer += 1
                break
    return answer
```

## \[WIP\] 지형편집

```python
from collections import defaultdict

def solution(land, P, Q):
    block_table = defaultdict(int)
    price = {}
    for l in land:
        for block in l:
            block_table[block] += 1

    def getPrice(target):
        if target not in price:
            price[target] = 0
            for block, count in block_table.items():
                if block < target:
                    price[target] += (target - block) * P * count
                else:
                    price[target] += (block - target) * Q * count
        return price[target]

    left = min(block_table)
    right = max(block_table)
    target = (right + left) // 2
    while left <= target <= right:
        if getPrice(target - 1) < getPrice(target) and getPrice(target + 1) < getPrice(target):
            if getPrice(target - 1) < getPrice(target + 1):
                target = target - 1
            else:
                target = target + 1
        if getPrice(target - 1) < getPrice(target):
            target = target - 1
        elif getPrice(target + 1) < getPrice(target):
            target = target + 1
        else:
            return getPrice(target)
    return 0
```

