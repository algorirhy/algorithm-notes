# [整数拆分](https://leetcode-cn.com/problems/integer-break)

### 方法一

贪心

```c++
class Solution {
    public int cuttingRope(int n) {
        if (n <= 3) return n - 1;
        int x = n / 3;
        int y = n % 3;
        if (y == 0) {
            return (int)Math.pow(3, x);
        } else if (y == 1) {
            return (int)Math.pow(3, x - 1) * 4;
        } else {
            return (int)Math.pow(3, x) * 2;
        }
    }
}
```

### 方法二

动态规划

```java
class Solution {
    public int cuttingRope(int n) {
        if (n <= 3) return n - 1;
        int[] dp = new int[n + 1];
        int res = 0; 
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        for (int i = 4; i <= n; i++) {
            // 避免重复计算
            for (int j = 1; j <= i / 2; j++) {
                res = Math.max(res, dp[j] * dp[i - j]);
            }
            dp[i] = res;
        }
        return dp[n];
    }
}
```

