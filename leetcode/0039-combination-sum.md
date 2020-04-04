# [组合总和](https://leetcode-cn.com/problems/combination-sum/)

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates , int target) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(candidates );
        backTrack(candidates, target, 0, res, new ArrayList<Integer>());
        return res;
    }

    private void backTrack(int[] candidates, int target, int index, List res, List tmp) {
        if (target < 0) return;
        if (target == 0) {
            res.add(new ArrayList(tmp));
            return;
        }
        for (int i = index; i < candidates.length; i++) {
            if (target < candidates[i]) break;
            tmp.add(candidates[i]);
            backTrack(candidates, target - candidates[i], i, res, tmp);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```

