# [反转字符串](https://leetcode-cn.com/problems/reverse-string/)

```java
class Solution {
    public void reverseString(char[] s) {
        if (s == null || s.length < 2) return;
        for (int i = 0, j = s.length - 1; i < j; i++, j--) {
            char c = s[i];
            s[i] = s[j];
            s[j] = c;
        }
    }
}
```

