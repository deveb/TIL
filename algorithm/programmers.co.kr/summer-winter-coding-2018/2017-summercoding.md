# 2017 SummerCoding

##  소수만들기

```python
def solution(nums):
    answer = 0
    for i in range(len(nums) - 2):
        for j in range(i + 1, len(nums) - 1):
            for k in range(j + 1, len(nums)):
                value = sum([nums[i], nums[j], nums[k]])
                count = 2
                primes = 0
                while count <= value:
                    if value % count == 0:
                        primes +=1
                        value = value // count 
                        count = 1
                    count += 1
                if primes == 1:
                    answer += 1
    return answer
```

## 점프와 순간이동

## 배달

## 기지국 설치

## 스티커 모으기

