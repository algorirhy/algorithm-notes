# [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

### 方法一

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        traversal(root, res);
        return res;
    }

    private void traversal(TreeNode root, List<Integer> res) {
        if (root == null) return;
        res.add(root.val);
        traversal(root.left, res);
        traversal(root.right, res);
    }
}
```

### 方法二

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Deque<TreeNode> s = new ArrayDeque<>();
        TreeNode cur = root;
        while (!s.isEmpty() || cur != null) {
            while(cur != null) {
                res.add(cur.val);
                s.push(cur);
                cur = cur.left;
            }
            cur = s.pop().right;
        }
        return res;
    }
}
```

### 方法三

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

    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Deque<ColorNode> stack = new ArrayDeque<>();
        stack.push(new ColorNode(root,"white"));

        while (!stack.isEmpty()) {
            ColorNode cNode = stack.pop();
            if (cNode.color == "white") {
                //右左根               
                if (cNode.node.right != null) {
                    stack.push(new ColorNode(cNode.node.right,"white"));
                }
                if (cNode.node.left != null) {
                    stack.push(new ColorNode(cNode.node.left,"white"));
                }
                stack.push(new ColorNode(cNode.node,"grey"));
            } else {
                res.add(cNode.node.val);
            }
        }
        return res;
    }
}
```

