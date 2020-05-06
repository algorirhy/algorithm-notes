# [最低票价](https://leetcode-cn.com/problems/minimum-cost-for-tickets/)

动态规划

```java
class Solution {
    public int mincostTickets(int[] days, int[] costs) {
        if (days == null || days.length == 10 || costs == null || costs.length == 0) {
            return 0;
        }
        int[] dp = new int[days[days.length - 1] + 1];
        for (int num : days) {
            dp[num] = 1;
        }
        for (int i = 1; i < dp.length; i++) {
            if (dp[i] == 0) {
                dp[i] = dp[i - 1];
                continue;
            }
            int cost1 = dp[i - 1] + costs[0];
            int cost2 = i > 7 ? dp[i - 7] + costs[1] : costs[1];
            int cost3 = i > 30 ? dp[i - 30] + costs[2] : costs[2];
            dp[i] = Math.min(Math.min(cost1, cost2), cost3);
        }
        return dp[dp.length - 1];
    }
}
```

