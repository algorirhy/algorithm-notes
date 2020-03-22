# [数字 1 的个数](https://leetcode-cn.com/problems/number-of-digit-one/)

数学问题，参考牛客讨论区用户[@Duqcuid](https://www.nowcoder.com/questionTerminal/bd7f978302044eee894445e244c7eee6?f=discussion)

```java
class Solution {
    public int countDigitOne(int n) {
        if (n == 0) return 0;
        int count = 0;
        for (long i = 1; i <= n; i *= 10) {
            long driver = i * 10;
            count += (n / driver) * i + Math.min(Math.max(n % driver - i + 1, 0), i);
        }
        return count;
    }
}
```
