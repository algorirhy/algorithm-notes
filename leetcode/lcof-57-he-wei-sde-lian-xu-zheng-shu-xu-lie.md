# [和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof)

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        int left = 1, right = 1;
        int sum = 0;
        List<int[]> res = new ArrayList<>();

        while (left <= target / 2) {
            if (sum < target) {
                sum += right;
                right++;
            } else if (sum > target) {
                sum -= left;
                left++;
            } else{
                int[] tmp = new int[right - left];
                for (int k = left; k < right; k++) {
                    tmp[k - left] = k;
                }
                res.add(tmp);

                sum -= left;
                left++;
            }
        }

        return res.toArray(new int[res.size()][]);
    }
}
```

