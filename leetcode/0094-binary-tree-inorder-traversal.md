# [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

### 方法一

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        traversal(root, res);
        return res;
    }

    private void traversal(TreeNode root, List<Integer> res) {
        if (root == null) return;
        traversal(root.left, res);
        res.add(root.val);
        traversal(root.right, res);
    }
}
```

### 方法二

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode p = root;
        while (p != null || !stack.isEmpty()) {
            while (p != null) {
                stack.push(p);
                p = p.left;
            }
            p = stack.pop();
            res.add(p.val);
            p = p.right;
        }
        return res;
    }
}
```

### 方法三

”颜色标记法“

* 使用颜色标记节点的状态，新节点为白色，已访问的节点为灰色。

* 如果遇到的节点为白色，则将其标记为灰色，然后将其右子节点、自身、左子节点依次入栈。

* 如果遇到的节点为灰色，则将节点的值输出。

  参考：[hzhu212](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/yan-se-biao-ji-fa-yi-chong-tong-yong-qie-jian-ming/)
  

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

    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Deque<ColorNode> stack = new ArrayDeque<>();
        stack.push(new ColorNode(root,"white"));

        while (!stack.isEmpty()) {
            ColorNode cNode = stack.pop();
            if (cNode.color == "white") {
                //右根左
                if (cNode.node.right != null) {
                    stack.push(new ColorNode(cNode.node.right,"white"));
                }
                stack.push(new ColorNode(cNode.node,"grey"));
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

