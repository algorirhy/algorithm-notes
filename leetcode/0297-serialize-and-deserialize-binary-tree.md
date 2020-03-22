# [二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

```java
public class Codec {
    public String serialize(TreeNode root) {
        if (root == null) return "[]";
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        StringBuilder sb = new StringBuilder();
        sb.append("[" + root.val);
        while(!queue.isEmpty()) {
            TreeNode node = queue.remove();
            if (node.left != null) {
                queue.add(node.left);
                sb.append("," + node.left.val);
            } else {
                sb.append(",null");
            }
            if (node.right != null) {
                queue.add(node.right);
                sb.append("," + node.right.val);
            } else {
                sb.append(",null");
            }
        }
        sb.append("]");
        return sb.toString();
    }

    public TreeNode deserialize(String data) {
        if (data.length() == 2) return null;
        data = data.substring(1, data.length() - 1);
        String[] vals = data.split(",");
        Deque<TreeNode> queue = new ArrayDeque<>();
        TreeNode root = new TreeNode(Integer.valueOf(vals[0]));
        queue.add(root);
        int index = 1;
        while(!queue.isEmpty()) {
            TreeNode node = queue.remove();
            if (vals[index].equals("null")) {
                node.left = null;
            } else {
                node.left = new TreeNode(Integer.valueOf(vals[index]));
                queue.add(node.left);
            }
            index++;
            if (vals[index].equals("null")) {
                node.right = null;
            } else {
                node.right = new TreeNode(Integer.valueOf(vals[index]));
                queue.add(node.right);
            }
            index++;
        }
        return root;
    }
}
```

