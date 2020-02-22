# [二叉搜索树的第k个结点](https://www.nowcoder.com/practice/ef068f602dde4d28aab2b210e859150a?tpId=13&tqId=11215&tPage=4&rp=4&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

```c++
class Solution {
public:
    TreeNode* KthNode(TreeNode* pRoot, int k){
        if(!pRoot || k <= 0)
            return nullptr;
        stack<TreeNode*> stk;
        int count = 0;
        TreeNode* node = pRoot;
        while(node || !stk.empty()){
            if(node){
                stk.push(node);
                node = node->left;
            }else{
                node = stk.top();
                stk.pop();
                count++;
                if(count == k)
                    return node;
                node = node->right;
            }
        }
        return nullptr;
    }
};
```

