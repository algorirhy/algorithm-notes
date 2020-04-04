# [组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/)

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
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
            // 去重
            if (i > index && candidates[i - 1] == candidates[i]) continue;
            tmp.add(candidates[i]);
            backTrack(candidates, target - candidates[i], i + 1, res, tmp);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```

