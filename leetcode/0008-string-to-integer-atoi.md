# [字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi) 

```java
class Solution {
    public int myAtoi(String str) {
        str = str.trim();
        int len = str.length();
        if (len == 0) return 0;
        int abs = 1;
        long res = 0;
        if (str.charAt(0) == '-') abs = -1;
        for (int i = (str.charAt(0) == '+' || str.charAt(0) == '-') ? 1 : 0; i < len; i++) {
            if (str.charAt(i) < '0' || str.charAt(i) > '9') break;
            res = res * 10 + (str.charAt(i)-'0');
            if (abs == 1 && res > Integer.MAX_VALUE) {
                return Integer.MAX_VALUE;
            } else if (abs == -1 && abs * res < Integer.MIN_VALUE) {
                return Integer.MIN_VALUE;
            }
        }
        return (int)(res * abs);
    }
}
```

