# [翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

### 方法一

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```

### 方法二

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (node.left != null || node.right != null) {
                TreeNode tmp = node.left;
                node.left = node.right;
                node.right = tmp;
            }
            if (node.left != null) stack.push(node.left);
            if (node.right != null) stack.push(node.right);
        }
        return root;
    }
}
```

### 方法三

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.remove();
            if (node.left != null || node.right != null) {
                TreeNode tmp = node.left;
                node.left = node.right;
                node.right = tmp;
            }
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        return root;
    }
}
```

