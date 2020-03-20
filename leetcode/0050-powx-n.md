# [Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

快速幂

```java
class Solution {
    public double myPow(double x, int n) {
        long p = n;
        double res = 1.0;
        if (p < 0) {
            x = 1 / x;
            p = -p;
        }
        while(p > 0) {
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
