# [有效数字](https://leetcode-cn.com/problems/valid-number/)

```java
class Solution {
    public boolean isNumber(String s) {
        s = s.trim();
        boolean hasPoint = false;
        boolean hasE = false;
        boolean hasNumber = false;
        boolean numberAfterE = true;

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) >= '0' && s.charAt(i) <= '9') {
                // e后面必须有数字
                hasNumber = true;
                numberAfterE = true;
            } else if (s.charAt(i) == '.') {
                // e后面不能接小数点，小数点不能出现两次
                if (hasE || hasPoint) {
                    return false;
                }
                hasPoint = true;
            } else if (s.charAt(i) == 'e' || s.charAt(i) == 'E') {
                // e只能出现异常，e前面必须有数字
                if (hasE || !hasNumber) {
                    return false;
                }
                hasE = true;
                numberAfterE = false;
            } else if (s.charAt(i) == '+' || s.charAt(i) == '-') {
                // 符号只能出现在开通或者e后面
                if (i != 0 && s.charAt(i - 1) != 'e' && s.charAt(i - 1) != 'E') {
                    return false;
                }
            } else {
                return false;
            }
        }
        return hasNumber && numberAfterE;
    }
}
```

