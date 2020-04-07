# [正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length(), n = p.length();
        // s 前 i 个字符[0,i)是否能匹配 p 的前 j 个字符[0,j)
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        // 判断 p 是否匹配空串
        for (int i = 2; i <= n; i++) {
            dp[0][i] = dp[0][i - 2] && p.charAt(i - 1) == '*';
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                char str = s.charAt(i - 1);
                char pat = p.charAt(j - 1);
                if (str == pat || pat == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (pat == '*') {
                    if (j >= 2) {
                        char prePat = p.charAt(j - 2);
                        if (prePat == str || prePat == '.') {
                            // 只有p[j-2]==s[i-1]或p[j-2]==‘.’才可以让*取1个或者多个字符
                            dp[i][j] = dp[i][j-1] || dp[i-1][j];
                        }
                        // 不论p[j-2]是否等于s[i-1]都可以删除掉j-1和j-2处字符
                        dp[i][j] = dp[i][j] || dp[i][j-2];
                    }
                } else {
                    dp[i][j] = false;
                }
            }
        }
        return dp[m][n];
    }
}
```

