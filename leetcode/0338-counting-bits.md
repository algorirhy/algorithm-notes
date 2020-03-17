# [比特位计数](https://leetcode-cn.com/problems/counting-bits/)

```java
class Solution {
    public int[] countBits(int num) {
        int[] res = new int[num + 1];
        res[0] = 0;
        for (int i = 1; i <= num; i++) {
            if ((i & 1) == 1) {
                // 二进制表示中，奇数一定比前面那个偶数多一个 1
                res[i] = res[i - 1] + 1;
            } else {
                // 二进制表示中，偶数中 1 的个数一定和除以 2 之后的那个数一样多
                res[i] = res[i >> 1];
            }
        }
        return res;
    }
}
```

