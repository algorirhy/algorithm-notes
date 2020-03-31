# [解码方法](https://leetcode-cn.com/problems/decode-ways/)

从后往前 动态规划 

```java
class Solution {
    public int numDecodings(String s) {
        if (s.equals("0")) return 0;
        int len = s.length();
        // dp[i]表示第i+1个字符到最后的解码方法数
        int[] dp = new int[len + 1];
        dp[len] = 1;
        // 最后一个数字不等于 0 就初始化为 1
        if (s.charAt(len - 1) != '0') {
            dp[len - 1] = 1;
        }
        for (int i = len - 2; i >= 0; i--) {
            if (s.charAt(i) == '0') {
                dp[i] = 0;
                continue;
            }
            if ((s.charAt(i) - '0') * 10 + (s.charAt(i + 1) - '0') <= 26) {
                dp[i] = dp[i + 1] + dp[i + 2];
            } else {
                dp[i] = dp[i + 1];
            }
        }
        return dp[0];
    }
}
```

空间优化

```java
class Solution {
    public int numDecodings(String s) {
        if (s.equals("0")) return 0;
        int len = s.length();
        // pre->res->next
        int res = 0, next = 1;
        // 最后一个数字不等于 0 就初始化为 1
        if (s.charAt(len - 1) != '0') {
            res = 1;
        }
        for (int pre = len - 2; pre >= 0; pre--) {
            if (s.charAt(pre) == '0') {
                next = res;
                res = 0;
                continue;
            }
            if ((s.charAt(pre) - '0') * 10 + (s.charAt(pre+ 1) - '0') <= 26) {
                res += next;
                // next 用来存储 res 以前的值
                next = res - next;
            } else {
                next = res;
            }
        }
        return res;
    }
}
```

