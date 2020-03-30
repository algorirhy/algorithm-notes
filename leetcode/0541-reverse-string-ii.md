# [反转字符串 II](https://leetcode-cn.com/problems/reverse-string-ii/)

```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] ch = s.toCharArray();
        for (int i = 0; i  ch.length; i += 2  k) {
            int begin = i, end = Math.min(i + k - 1, ch.length - 1);
            while (begin  end) {
                char tmp = ch[begin];
                ch[begin++] = ch[end];
                ch[end--] = tmp;
            }
        }
        return new String(ch);
    }
}
```

