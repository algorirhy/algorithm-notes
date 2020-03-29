# [三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

动态规划

定义状态：`dp[i][j]`表示包含第i行第j列元素的最小路径和

状态迁移方程：`dp[i][j] = min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle[i][j]`

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        // 自底向上
        int level = triangle.size();
        int[][] dp = new int[level + 1][level + 1];
        for (int i = level - 1; i >= 0; i--) {
            // i 层有 i + 1 个元素
            for (int j = 0; j <= i; j++) {
                dp[i][j] = Math.min(dp[i+1][j], dp[i+1][j+1]) + triangle.get(i).get(j);
            }
        }
        return dp[0][0];
    }
}
```

空间优化

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        // 自底向上
        int level = triangle.size();
        int[] dp = new int[level + 1];
        for (int i = level - 1; i >= 0; i--) {
            // i 层有 i + 1 个元素
            for (int j = 0; j <= i; j++) {
                dp[j] = Math.min(dp[j], dp[j + 1]) + triangle.get(i).get(j);
            }
        }
        return dp[0];
    }
}
```

