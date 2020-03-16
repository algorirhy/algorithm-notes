# [字符串压缩](https://leetcode-cn.com/problems/compress-string-lcci/)

```java
class Solution {
    public String compressString(String S) {
        int len = S.length();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < len; ) {
            int j = i;
            while (j < len && S.charAt(j) == S.charAt(i)) {
                j++;
            }
            sb.append(S.charAt(i));
            sb.append(j-i);
            i = j;
        }
        if (sb.length() < S.length()) {
            return sb.toString();
        }
        return S;
    }
}
```