# [每个元音包含偶数次的最长子字符串](https://leetcode-cn.com/problems/find-the-longest-substring-containing-vowels-in-even-counts)

```java
class Solution {
    public int findTheLongestSubstring(String s) {
        int[] pre = new int[32];
        Arrays.fill(pre, Integer.MAX_VALUE);
        pre[0] = -1;
        int len = s.length();
        int status = 0, res = 0;
        for (int i = 0; i < len; i++) {
            switch (s.charAt(i)) {
                case 'a' : 
                    status ^= 1;
                    break;
                case 'e' : 
                    status ^= 2;
                    break;
                case 'i' : 
                    status ^= 4;
                    break;
                case 'o' : 
                    status ^= 8;
                    break;
                case 'u' : 
                    status ^= 16;
                    break;
                default:
                    break;
            }
            if (pre[status] == Integer.MAX_VALUE) {
                pre[status] = i;
            } else {
                res = Math.max(res, i - pre[status]);
            }
        }
        return res;
    }
}
```

