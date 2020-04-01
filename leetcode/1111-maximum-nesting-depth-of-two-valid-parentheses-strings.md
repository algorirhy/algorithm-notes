# [有效括号的嵌套深度](https://leetcode-cn.com/problems/maximum-nesting-depth-of-two-valid-parentheses-strings/)

```java
class Solution {
    public int[] maxDepthAfterSplit(String seq) {
        int[] res = new int[seq.length()];
        int index = 0;
        for (char ch : seq.toCharArray()) {
            res[index++] = (ch == '(') ? (index & 1) : ((index + 1) & 1);
        }
        return res;
    }
}
```

