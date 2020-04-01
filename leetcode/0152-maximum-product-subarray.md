# [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

动态规划

```java
class Solution {
    public int maxProduct(int[] nums) {
        int res = Integer.MIN_VALUE;
        int min = 1, max = 1;
        for (int i = 0; i < nums.length; i++) {
            // 乘以负数，交换 min 与 max
            if (nums[i] < 0) {
                int tmp = min;
                min = max;
                max = tmp;
            }
            min = Math.min(min * nums[i], nums[i]);
            max = Math.max(max * nums[i], nums[i]);
            res = Math.max(res, max);
        }
        return res;
    }
}
```

