# [路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new LinkedList<>();
        findPath(root, sum, res, new LinkedList<Integer>());
        return res;
    }

    private void findPath(TreeNode root, int sum, List<List<Integer>> res, List<Integer> tmp) {
        if (root == null) return;
        tmp.add(root.val);
        if (root.left == null && root.right == null && root.val == sum) {
            res.add(new LinkedList<>(tmp));
        }
        findPath(root.left, sum - root.val, res, tmp);
        findPath(root.right, sum - root.val, res, tmp);
        tmp.remove(tmp.size() - 1);
    }
}
```

