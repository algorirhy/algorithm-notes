# [全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

```java
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> res = new ArrayList<>();

    public List<List<Integer>> permuteUnique(int[] nums) {
        int len = nums.length;
        if (len == 0) return res;
        Arrays.sort(nums);
        boolean[] visited = new boolean[len];
        backTrack(nums, visited);
        return res;
    }

    private void backTrack(int[] nums, boolean[] visited) {
        if (path.size() == nums.length) {
            res.add(new ArrayList(path));
        }
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            if (i > 0 && nums[i - 1] == nums[i] && !visited[i - 1]) {
                continue;
            }
            path.add(nums[i]);
            visited[i] = true;
            backTrack(nums, visited);
            visited[i] = false;
            path.remove(path.size() - 1);
            
        }
    }
}
```

