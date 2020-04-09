# [最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)

滑动窗口

```java
class Solution {
    public String minWindow(String s, String t) {
        int start = 0, minLen = Integer.MAX_VALUE;
        int left = 0, right = 0;
        int match = 0;
        Map<Character, Integer> window  = new HashMap<>();
        Map<Character, Integer> needs  = new HashMap<>();
        for (char c : t.toCharArray()) {
            needs.put(c, needs.getOrDefault(c, 0) + 1);
        }
        while (right < s.length()) {
            char c1 = s.charAt(right);
            if (needs.containsKey(c1)) {
                window.put(c1, window.getOrDefault(c1, 0) + 1);
                // 该字符出现的次数达到要求
                if (window.get(c1).compareTo(needs.get(c1)) == 0) {
                    match++;
                }
            }
            right++;
            // 如果满足要求了，left向右缩小范围
            while (match == needs.size()) {
                // 更新最小值
                if (right - left < minLen) {
                    start = left;
                    minLen = right - left;
                }
                char c2 = s.charAt(left);
                if (needs.containsKey(c2)) {
                    window.put(c2, window.get(c2) - 1);
                    if (window.get(c2) < needs.get(c2)) {
                        match--;
                    }
                }
                left++;
            }
        }
        return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
    }
}
```

