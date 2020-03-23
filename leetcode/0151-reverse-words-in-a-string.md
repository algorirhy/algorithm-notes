# [翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string)

```java
class Solution {
    public String reverseWords(String s) {
        s = s.trim();
        StringBuffer sb = new StringBuffer();
        int end = s.length();
        for (int begin = s.length() - 1; begin >= 0; begin--) {
            if (s.charAt(begin) == ' ') {
                sb.append(s.substring(begin + 1, end) + ' ');
                while (s.charAt(begin) == ' ') begin--;
                end = begin + 1;
            }
        }
        return sb.append(s.substring(0, end)).toString();
    }
}
```

