# [另一个树的子树](https://leetcode-cn.com/problems/subtree-of-another-tree/)

```java
class Solution {
    public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null || t == null) return false;
        boolean res = checkSubtree(s, t);
        if (!res) {
            res = isSubtree(s.left, t);
        }
        if (!res) {
            res = isSubtree(s.right, t);
        }
        return res;
    }

    private boolean checkSubtree(TreeNode a, TreeNode b) {
        if (a == null && b == null) return true;
        if (a == null || b == null) return false;
        if (a.val != b.val) return false;
        return checkSubtree(a.left, b.left) && checkSubtree(a.right, b.right);
    }
}
```

