# [从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

### 方法一

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        int depth = 0;
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) return res;
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> tier = new ArrayList<>(size);
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.remove();
                if ((depth & 1) == 0) {
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

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (root == null) return res;
        Deque<TreeNode> stack1 = new ArrayDeque<>();
        Deque<TreeNode> stack2 = new ArrayDeque<>();
        stack1.push(root);
        while (!stack1.isEmpty() || !stack2.isEmpty()) {
            List<Integer> list1 = new ArrayList<>();
            List<Integer> list2 = new ArrayList<>();
            TreeNode cur = null;
            while(!stack1.isEmpty()) {
                cur = stack1.pop();
                list1.add(cur.val);
                if (cur.left != null) stack2.push(cur.left);
                if (cur.right != null) stack2.push(cur.right);
            }
            if (!list1.isEmpty()) res.add(list1);
            while (!stack2.isEmpty()) {
                cur = stack2.pop();
                list2.add(cur.val);
                // 注意顺序反了
                if (cur.right != null) stack1.push(cur.right);
                if (cur.left != null) stack1.push(cur.left);
            }
            if (!list2.isEmpty()) res.add(list2);
        }
        return res;
    }
}
```

