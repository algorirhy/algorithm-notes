# [二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

### 方法一

递归

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```



### 方法二

层次遍历

```java
class Solution {
    public int maxDepth(TreeNode root) {
        int depth = 0;
        if (root == null) return depth;
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            depth++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.remove();
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
        }
        return depth;
    }
}
```



