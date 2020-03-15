# [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)

### 方法一

```java
class Solution {
    TreeNode pre = null;

    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        if (!isValidBST(root.left)) return false;
        if (pre != null && pre.val >= root.val) return false;
        pre = root;
        return isValidBST(root.right);
    }
}
```

### 方法二

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode p = root;
        TreeNode pre = null;
        while (p != null || !stack.isEmpty()) {
            while (p != null) {
                stack.push(p);
                p = p.left;
            }
            p = stack.pop();
            if (pre != null && pre.val >= p.val) {
                return false;
            }
            pre = p;
            p = p.right;
        }
        return true;
    }
}
```

### 方法三

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean isBST(TreeNode root, long  lower, long  upper) {
        if (root == null) return true;
        if (root.val <= lower || root.val >= upper) return false;
        return isBST(root.left, lower, root.val) && isBST(root.right, root.val, upper);
    }
}
```

