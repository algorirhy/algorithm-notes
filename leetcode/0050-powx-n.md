# [Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

### 方法一

二分递归

```java
class Solution {
    public double myPow(double x, int n) {
        if (n == 0) return 1;
        if (n == 1) return x;
        if (n == -1) return 1 / x;
        double half = myPow(x, n / 2);
        double rest = myPow(x, n % 2);
        return half * half * rest;
    }
}
```

### 方法二

快速幂

```java
class Solution {
    public double myPow(double x, int n) {
        long p = n;
        double res = 1.0;
        if (p < 0) {
            p = -p;
            x = 1 / x;
        }
        while (p > 0) {
            if ((p & 1) == 1) {
                res *= x;
            }
            x *= x;
            p >>= 1;
        }
        return res;
    }
}
```
