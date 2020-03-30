# [反转字符串中的单词 III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)

```java
public class Solution {
    public String reverseWords(String s) {
        String[] words = s.split(" ");
        StringBuilder res = new StringBuilder();
        for (String word: words)
            res.append(new StringBuffer(word).reverse().toString() + " ");
        return res.toString().trim();
    }
}
```

