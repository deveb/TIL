# Fibonacci

### 43104

```python
def solution(N):
    def fib(n):
        fib = [1, 1]
        if not n in fib:
            for i in range(len(fib), n+1):
                fib.append(fib[i-2] + fib[i-1])
        return fib[n]
    return fib(N-1)*2 + fib(N)*2
```

