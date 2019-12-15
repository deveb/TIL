# karatsuba

```python
# A = 1234
# B = 5678
A = 3141592653589793238462643383279502884197169399375105820974944592
B = 2718281828459045235360287471352662497757247093699959574966967627


def count_digits(number):
    digits = 0
    while number:
        number = number // 10
        digits += 1
    return digits


def karatsuba(A, B):
    digits = max(count_digits(A), count_digits(B))
    if digits <= 1:
        return A * B
    half_digits = digits // 2

    a = A // 10 ** half_digits
    b = A % 10 ** half_digits
    c = B // 10 ** half_digits
    d = B % 10 ** half_digits

    ac = karatsuba(a, c)
    bd = karatsuba(b, d)
    ad_bc = karatsuba(a + b, c + d) - ac - bd
    return ac * 10 ** (2*half_digits) + ad_bc * 10 ** half_digits + bd


print(karatsuba(A, B))
# 8539734222673567065463550869546574495034888535765114961879601127067743044893204848617875072216249073013374895871952806582723184
```

