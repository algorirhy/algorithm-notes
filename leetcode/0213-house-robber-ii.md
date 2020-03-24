# [打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

```java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if (len == 0) return 0;
        if (len == 1) return nums[0];
        return Math.max(myRob(nums, 0, len - 1), myRob(nums, 1, len));
    }

    private int myRob(int[] nums, int start, int end) {
        int a = 0, b = 0;
        for (int i = start; i < end; i++) {
            int c = Math.max(b, a + nums[i]);
            a = b;
            b = c;
        }
        return b;
    }
}
```

