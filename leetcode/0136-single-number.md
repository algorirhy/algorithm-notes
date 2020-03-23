# [只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

与两个相同的数进行异或运算，值不变。

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int num : nums) {
            res ^= num;
        }
        return res;
    }
}
```

