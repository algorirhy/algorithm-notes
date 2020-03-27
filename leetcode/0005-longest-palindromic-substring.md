# [最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring)

### 方法一

动态规划

`dp[i][j]` 表示子串 `s[i, j]` 是否为回文子串

```java
class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        if (len < 2) return s;
        boolean[][] dp = new boolean[len][len];
        for (int i = 0; i < len; i++) {
            dp[i][i] = true;
        }
        int maxLen = 1; 
        int start = 0;
        for (int end = 1; end < len; end++) {
            for (int begin = 0; begin < end; begin++) {
                if (s.charAt(begin) == s.charAt(end)) {
                    if (end - begin < 3) {
                        dp[begin][end] = true;
                    } else {
                        dp[begin][end] = dp[begin + 1][end - 1];
                    }
                } else {
                    dp[begin][end] = false;
                }
                if (dp[begin][end]) {
                    if (maxLen < end - begin + 1) {
                        start = begin;
                        maxLen = end - begin + 1;
                    }
                }
            }
        }
        return s.substring(start, start + maxLen);
    }
}
```

### 方法二

中心扩散法

```java
class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        if (len < 2) return s;
        int maxLen = 1;
        String res = s.substring(0, 1);
        // 中心位置枚举到 len - 2 即可
        for (int i = 0; i < len - 1; i++) {
            String oddStr = centerSpread(s, i, i);
            String evenStr = centerSpread(s, i, i + 1);
            String maxLenStr = oddStr.length() > evenStr.length() ? oddStr : evenStr;
            if (maxLenStr.length() > maxLen) {
                maxLen = maxLenStr.length();
                res = maxLenStr;
            }
        }
        return res;
    }

    private String centerSpread(String s, int begin, int end) {
        int len = s.length();
        while (begin >= 0 && end < len) {
            if (s.charAt(begin) == s.charAt(end)) {
                begin--;
                end++;
            } else{
                break;
            }
        }
        // 注意 begin + 1
        return s.substring(begin + 1, end);
    }
}
```

