# Heap

### 42626

```python
import heapq
def solution(scoville, K):
    heapq.heapify(scoville)
    # 삽입/꺼내기 O(log n)
    # 배열로부터 힙 O(n log n) 최적은 O(n)
    answer = 0
    while scoville[0] < K:
        if len(scoville) == 1:
            return -1
        first = heapq.heappop(scoville)
        second = heapq.heappop(scoville)
        heapq.heappush(scoville, first + second*2)
        answer +=1
    return answer
```

### 42629

```python
import heapq
def solution(stock, dates, supplies, k):
    answer = 0
    heap = []
    for i, date in enumerate(dates):
        heapq.heappush(heap, (-supplies[i], date))
    while stock < k:
        answer += 1
        remains = []
        while heap:
            supply, date = heapq.heappop(heap)
            if stock >= date:
                stock += -supply
                break
            remains.append((supply, date))
        while remains:
            heapq.heappush(heap, remains.pop())
    return answer
```

