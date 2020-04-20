# [子集 II](https://leetcode-cn.com/problems/subsets-ii/)

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        backTrack(nums, 0, res, new ArrayList<>());
        return res;
    }

    private void backTrack(int[] nums, int index, List res, List tmp) {
        res.add(new ArrayList(tmp));
        for (int i = index; i < nums.length; i++) {
            // 去重
            if (i > index && nums[i - 1] == nums[i]) continue;
            tmp.add(nums[i]);
            backTrack(nums, i + 1, res, tmp);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```

