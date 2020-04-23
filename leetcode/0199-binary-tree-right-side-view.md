# [二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)

### 方法一

递归

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        helper(root, 0, res);
        return res;
    }

    private void helper(TreeNode root, int level, List<Integer> res) {
        if (root == null) return;
        if (res.size() == level) res.add(root.val);
        helper(root.right, level + 1, res);
        helper(root.left, level + 1, res);
    }
}
```

### 方法二

层次遍历

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            res.add(queue.peekLast().val);
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode tmp = queue.poll();
                if (tmp.left != null) queue.offer(tmp.left);
                if (tmp.right != null) queue.offer(tmp.right);
            }
        }
        return res;
    }
}
```

