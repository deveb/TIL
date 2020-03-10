# inversions

```python
from collections import deque


file = open('./IntegerArray.txt', 'r')
A = [int(line) for line in file.read().split('\n')]
file.close()
# A = [1, 3, 7, 2, 4, 6]


def merge_and_count_split_inv(B, C):
	D = []
	inv = 0
	B = deque(B)
	C = deque(C)
	while B and C:
		if B[0] < C[0]:
			D.append(B.popleft())
		else:
			D.append(C.popleft())
			inv += len(B)
	D = D + list(B) + list(C)
	return D, inv


def sort_and_count(A):
	if len(A) == 1:
		return A, 0

	half = len(A)//2
	B, X = sort_and_count(A[:half])
	C, Y = sort_and_count(A[half:])
	D, Z = merge_and_count_split_inv(B, C)
	return D, X + Y + Z


print(sort_and_count(A)[1])
# 2407905288
```

