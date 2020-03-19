# [最长回文串](https://leetcode-cn.com/problems/longest-palindrome/)

```java
class Solution {
    public int longestPalindrome(String s) {
        // A ~ Z: 65 ~ 90  a ~ z: 97 ~ 122
        int[] cnt = new int[58];
        for (char c : s.toCharArray()) {
            cnt[c - 'A'] += 1;
        }
        int res = 0;
        for (int num : cnt) {
            res += num - (num & 1);
        }
        return res < s.length() ? res + 1 : res;
    }
}
```

