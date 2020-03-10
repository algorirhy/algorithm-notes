# [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

### 方法一

深度优先搜索 / 回溯

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if (n == 0) return res;
        dfs("", 0, 0, n, res);
        return res;
    }

    private void dfs(String str, int left, int right, int n, List<String> res) {
        if (left == n && right == n) {
            res.add(str);
            return;
        }

        if (left < right) return;
        if (left < n) dfs(str + "(", left + 1, right, n, res);
        if (right < n) dfs(str + ")", left, right + 1, n, res);
    }
}
```

深度优先搜索

```java
class Solution {
    
    class Node {
        private String str;
        private int left, right;

        public Node(String str, int left, int right) {
            this.str = str;
            this.left = left;
            this.right = right;
        }
    }

    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if (n == 0) return res;
        Deque<Node> stack = new ArrayDeque<>();
        stack.add(new Node("", n, n));
        while (!stack.isEmpty()) {
            Node curNode = stack.pop();
            if (curNode.left == 0 && curNode.right == 0) {
                res.add(curNode.str);
            }
            if (curNode.left > 0) {
                stack.add(new Node(curNode.str + "(", curNode.left - 1, curNode.right));
            }
            if (curNode.right > 0 && curNode.left < curNode.right) {
                stack.add(new Node(curNode.str + ")", curNode.left, curNode.right - 1));
            }
        }
        return res;
    }
}
```



### 方法二

广度优先搜索

```java
class Solution {
    
    class Node {
        private String str;
        private int left, right;

        public Node(String str, int left, int right) {
            this.str = str;
            this.left = left;
            this.right = right;
        }
    }

    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if (n == 0) return res;
        Deque<Node> queue = new ArrayDeque<>();
        queue.add(new Node("", n, n));
        while (!queue.isEmpty()) {
            Node curNode = queue.remove();
            if (curNode.left == 0 && curNode.right == 0) {
                res.add(curNode.str);
            }
            if (curNode.left > 0) {
                queue.add(new Node(curNode.str + "(", curNode.left - 1, curNode.right));
            }
            if (curNode.right > 0 && curNode.left < curNode.right) {
                queue.add(new Node(curNode.str + ")", curNode.left, curNode.right - 1));
            }
        }
        return res;
    }
}
```



### 方法三

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

