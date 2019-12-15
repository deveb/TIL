# Stack/Queue

### 42583

```python
def solution(bridge_length, weight, truck_weights):
    on_the_bridge = [0] * bridge_length
    tick = 0
    while truck_weights:
        weight += on_the_bridge.pop(0)
        truck = 0 # 0 means no truck on the bridge
        if weight - truck_weights[0] > -1:
            truck = truck_weights.pop(0)
        weight -= truck
        on_the_bridge.append(truck)
        tick +=1
    return tick + bridge_length
```

### 42585

```python
from collections import deque
def solution(arrangement):
    answer = 0
    depth = 0
    queue = deque(arrangement)
    before = None
    while queue:
        popped = queue.popleft()
        depth = popped == '(' and depth + 1 or depth - 1
        if (before == popped == '(') or (before == popped == ')'):
            answer +=1
        elif before ==')' and popped == '(':
            answer += depth -1
        before = popped
    return answer
```

### 42587

```python
def solution(priorities, location):
    printed = []
    pp = [(index, number) for index, number in enumerate(priorities)]
    while pp:
        while pp[0][1] < max([number for __, number in pp]):
            rotate = pp.pop(0)
            pp.append(rotate)
        printed.append(pp.pop(0))
    return printed.index((location, priorities[location])) + 1
```

