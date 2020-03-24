# [打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)

```java
class Solution {
    public int rob(TreeNode root) {
        int[] res = getRob(root);
        return Math.max(res[0], res[1]);
    }

    private int[] getRob(TreeNode root) {
        if (root == null) return new int[]{0, 0};
        int[] left = getRob(root.left);
        int[] right = getRob(root.right);
        // 抢
        int rob = root.val + left[0] + right[0];
        // 不抢
        int not_rob = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
        return new int[]{not_rob, rob};
    }
}
```

