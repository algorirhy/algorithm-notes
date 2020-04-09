# [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

### 方法一

深度优先搜索 / 回溯

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        backTrack(n, n, res, "");
        return res;
    }

    private void backTrack(int left, int right, List res, String tmp) {
        if (left == 0 && right == 0) {
            res.add(tmp);
            return;
        }
        if (left > 0) backTrack(left - 1, right, res, tmp + "(");
        if (right > left) backTrack(left, right - 1, res, tmp + ")");
    }
}
```

### 方法二

动态规划

`dp[i]`：使用 `i` 对括号能够生成的组合。

```
dp[i] = "(" + dp[j] + ")" + dp[i- j - 1] , j = 0, 1, ..., i - 1
```

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        if (n == 0) return new ArrayList<>();
        List<List<String>> dp = new ArrayList<>(n);
        List<String> dp0 = new ArrayList<>();
        dp0.add("");
        dp.add(dp0);
        for (int i = 1; i <= n; i++) {
            List<String> cur = new ArrayList<>();
            for (int j = 0; j < i; j++) {
                List<String> str1 = dp.get(j);
                List<String> str2 = dp.get(i - j - 1);
                for (String s1 : str1) {
                    for (String s2 : str2) {    
                        cur.add("(" + s1 + ")" + s2);
                    }
                }
            }
            dp.add(cur);
        }
        return dp.get(n);
    }
}
```

