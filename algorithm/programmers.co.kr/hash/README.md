# Hash

{% page-ref page="42576.md" %}

### 42578

```python
from collections import Counter

def solution(clothes):
    clothes_by_part = Counter([p for _, p in clothes])
    answer = 1
    for _, cs in clothes_by_part.items():
        answer *= cs + 1
    return answer-1
```

### 42579

```python
def solution(genres, plays):
    indexes_by_plays = {p: [] for p in plays}
    plays_by_genre = {g: [] for g in genres}
    for i, p in enumerate(plays):
        indexes_by_plays[p].append(i)
        indexes_by_plays[p] = sorted(indexes_by_plays[p])
        plays_by_genre[genres[i]].append(p)
        plays_by_genre[genres[i]] = sorted(plays_by_genre[genres[i]], reverse=True)
    plays_by_genre = sorted(plays_by_genre.items(), key=lambda x: -sum(x[1]))
    
    answer = []
    for _, ps in plays_by_genre:
        for p in ps[:2]:
            answer += indexes_by_plays[p]
            if len(indexes_by_plays[p]) > 1:
                break
    return answer
```

### 43577

```python
def solution(phone_book):
    phone_book = sorted(phone_book, key= lambda x: len(x))
    for index in range(len(phone_book)):
        for p in phone_book[index+1:]:
            if p.startswith(phone_book[index]):
                return False
    return True
```

