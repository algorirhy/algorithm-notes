# [最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence)

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }
        int res = 0;
        for (int num : set) {
            if (!set.contains(num - 1)) {
                int curNum = num;
                int max = 1;
                while (set.contains(curNum + 1)) {
                    curNum++;
                    max++;
                }
                res = Math.max(max, res);
            }
        }
        return res;
    }
}
```

