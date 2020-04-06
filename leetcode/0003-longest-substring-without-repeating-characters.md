# [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

滑动窗口

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s.length() == 0) return 0;
        Map<Character, Integer> map = new HashMap<>();
        int max = 0;
        for (int left = 0, right = 0; right < s.length(); right++) {
            char ch = s.charAt(right);
            if (map.containsKey(ch)) {
                // 判断上次出现该字符是否是在 left 之后
                left = Math.max(left, map.get(ch));
            }
            map.put(ch, right + 1);
            max = Math.max(max, right - left + 1);
        }
        return max;
    }
}
```
