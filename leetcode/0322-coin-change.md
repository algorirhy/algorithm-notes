# [零钱兑换](https://leetcode-cn.com/problems/coin-change/)

### 方法一

贪心 + DFS

```java
class Solution {
    private int res = Integer.MAX_VALUE;
    
    public int coinChange(int[] coins, int amount) {
        if(amount == 0) return 0;
        Arrays.sort(coins);
        change(coins, amount, coins.length - 1, 0);
        return res == Integer.MAX_VALUE ? -1 : res;
    }

    private void change(int[] coins, int amount, int index, int count) {
        if (amount == 0) {
            res = Math.min(res, count);
            return;
        }
        if (index < 0) return;
        for (int k = amount / coins[index]; k >= 0 && count + k < res; k--) {
            change(coins, amount - k * coins[index], index - 1, count + k);
        }
    }
}
```

### 方法二

动态规划

f(n) = min{f(n-1), f(n-2), f(n-5)} + 1

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```

