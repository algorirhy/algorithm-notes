# [买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        int min_price = prices[0];
        int max_profit = 0;
        for (int i = 1; i < prices.length; i++) {
            max_profit = Math.max(prices[i] - min_price, max_profit);
            min_price = Math.min(prices[i], min_price);
        }
        return max_profit;
    }
}
```

