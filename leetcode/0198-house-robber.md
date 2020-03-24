# [打家劫舍](https://leetcode-cn.com/problems/house-robber)

### 方法一

动态规划

```java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if (len == 0) return 0;
        int[] dp = new int[len + 1];
        dp[0] = 0;
        dp[1] = nums[0];
        for (int i = 2; i <= len; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i - 1]);
        }
        return dp[len];
    }
}
```

### 方法二

状态压缩

```java
class Solution {
    public int rob(int[] nums) {
        int a = 0, b = 0;
        for (int i = 0; i < nums.length; i++) {
            int c = Math.max(b, a + nums[i]);
            a = b;
            b = c;
        }
        return b;
    }
}
```

