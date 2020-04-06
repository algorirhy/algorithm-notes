# [二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

### 方法一

递归

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        traversal(root, res);
        return res;
    }

    private void traversal(TreeNode root, List<Integer> res) {
        if (root == null) return;
        traversal(root.left, res);
        traversal(root.right, res);
        res.add(root.val);
    }
}
```

### 方法二

标准解法

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Deque<TreeNode> s = new ArrayDeque<>();
        TreeNode pre = null;
        TreeNode cur = root;
        while (!s.isEmpty() || cur != null) {
            while (cur != null) {
                s.push(cur);
                cur = cur.left;
            }
            cur = s.peek();
            // 若没有右节点或者右节点已经访问过，则输出该节点值
            if (cur.right == null || pre == cur.right) {
                s.pop();
                res.add(cur.val);
                pre = cur;
                cur = null;
            } else {
                cur = cur.right;
            }
        }
        return res;
    }
}
```

### 方法三

前序遍历顺序为：根 -> 左 -> 右

后序遍历顺序为：左 -> 右 -> 根

* 将前序遍历中节点插入结果链表尾部的逻辑，修改为将节点插入结果链表的头部，那么结果链表就变为了：右 -> 左 -> 根

* 再将遍历的顺序由从左到右修改为从右到左，那么结果链表就变为了：左 -> 右 -> 根

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> res = new LinkedList<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode p = root;
        while (p != null || !stack.isEmpty()) {
            while (p != null) {
                res.addFirst(p.val);
                stack.push(p);
                p = p.right;
            }
            p = stack.pop().left;
        }
        return res;
    }
}
```

### 方法三

颜色节点

```java
class Solution {

    class ColorNode {
        TreeNode node;
        String color;
        
        public ColorNode(TreeNode node,String color){
            this.node = node;
            this.color = color;
        }
    }

    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Deque<ColorNode> stack = new ArrayDeque<>();
        stack.push(new ColorNode(root,"white"));

        while (!stack.isEmpty()) {
            ColorNode cNode = stack.pop();
            if (cNode.color == "white") {
                //根右左
                stack.push(new ColorNode(cNode.node,"grey"));                
                if (cNode.node.right != null) {
                    stack.push(new ColorNode(cNode.node.right,"white"));
                }
                if (cNode.node.left != null) {
                    stack.push(new ColorNode(cNode.node.left,"white"));
                }
            } else {
                res.add(cNode.node.val);
            }
        }
        return res;
    }
}
```

