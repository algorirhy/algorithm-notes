# [转换成小写字母](https://leetcode-cn.com/problems/to-lower-case/)

```java
class Solution {
    public static String toLowerCase(String str) {
        char[] ch = str.toCharArray();
        for (int i = 0; i < ch.length; i++) {
            if (ch[i] >= 'A' && ch[i] <= 'Z') {
                ch[i] += 32;
            }
        }
        //return new String(ch);
        return String.valueOf(ch);
    }
}
```

