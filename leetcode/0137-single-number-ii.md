# [只出现一次的数字 II](https://leetcode-cn.com/problems/single-number-ii/)

```java
class Solution {
    public int singleNumber(int[] nums) {
        int a = 0, b = 0;
        for (int num : nums) {
            a = a ^ num & ~b;
            b = b ^ num & ~a;
        }
        return a;
    }
}
```

