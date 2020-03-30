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
        TreeNode cur = root;
        TreeNode pre = null;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            if (pre != null && pre.val >= cur.val) {
                return false;
            }
            pre = cur;
            cur = cur.right;
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

