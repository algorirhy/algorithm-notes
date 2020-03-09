# [单词拆分](https://leetcode-cn.com/problems/word-break/)

### 方法一

#### 记忆化回溯

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return wordHelper(s, new HashSet(wordDict), 0, new Boolean[s.length()]);
    }

    private boolean wordHelper(String s, Set<String> wordSet, int pos, Boolean[] memo) {
        if (pos == s.length()) {
            return true;
        }
        if (memo[pos] != null) {
            return memo[pos];
        }
        for (int end = pos + 1; end <= s.length(); end++) {
            if (wordSet.contains(s.substring(pos, end)) 
                    && wordBreakHelper(s, wordSet, end, memo)){
                return memo[pos] = true;
            }
        }
        return memo[pos] = false;
    }
}
```

### 方法二

动态规划

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int len = s.length();
        boolean[] dp = new boolean[len + 1];
        Set<String> wordSet = new HashSet(wordDict);
        //空格在wordDict中
        dp[0] = true;
        for (int i = 1; i <= len; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[len];
    }
}
```

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int len = s.length();
        boolean[] dp = new boolean[len + 1];
        Set<String> wordSet = new HashSet(wordDict);
        for (int i = 1; i <= len; i++) {
            //前i个字符组成的单词在wordDict中
            if (wordSet.contains(s.substring(0, i))) {
                dp[i] = true;
                continue;
            }
            for (int j = 1; j < i; j++) {
                if (dp[j] && wordSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[len];
    }
}
```

