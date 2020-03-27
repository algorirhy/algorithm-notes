# [平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return check(root) != -1;
    }

    private int check(TreeNode root) {
        if (root == null) return 0;
        int left = check(root.left);
        int right = check(root.right);
        if (left == -1 || right == -1) return -1;
        return Math.abs(left - right) > 1 ? -1 : 1 + Math.max(left, right);
    }
}
```

