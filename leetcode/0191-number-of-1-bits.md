# [位1的个数](https://leetcode-cn.com/problems/number-of-1-bits/)

```java
public class Solution {
    public int hammingWeight(int n) {
        int res = 0;
        while (n != 0) {
            res++;
            n &= n - 1;
        }
        return res;
    }
}
```

