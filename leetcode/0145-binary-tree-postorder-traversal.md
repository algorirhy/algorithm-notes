# [二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

### 方法一

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

