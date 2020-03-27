# [二叉树的锯齿形层次遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

### 方法一

层次遍历，按层讨论

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        int depth = 0;
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) return res;
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> tier = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.remove();
                if (depth % 2 == 0) {
                    tier.add(node.val);
                } else {
                    tier.add(0, node.val);
                }
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
            depth++;
            res.add(tier);
        }
        return res;
    }
}
```

### 方法二

层次遍历，两个栈轮流打印

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) return res;
        Deque<TreeNode> stack1 = new ArrayDeque<>();
        Deque<TreeNode> stack2 = new ArrayDeque<>();
        stack1.push(root);
        while(!stack1.isEmpty() || !stack2.isEmpty()) {
            List<Integer> list1 = new ArrayList<>();
            List<Integer> list2 = new ArrayList<>();
            TreeNode cur = null;
            while (!stack1.isEmpty()) {
                cur = stack1.pop();
                if (cur.left != null) stack2.push(cur.left);
                if (cur.right != null) stack2.push(cur.right);
                list1.add(cur.val);
            }
            if (!list1.isEmpty()) res.add(list1);

            while (!stack2.isEmpty()) {
                cur = stack2.pop();
                if (cur.right != null) stack1.push(cur.right);
                if (cur.left != null) stack1.push(cur.left);
                list2.add(cur.val);
            }
            if (!list2.isEmpty()) res.add(list2);
        }
        return res;
    }
}
```

