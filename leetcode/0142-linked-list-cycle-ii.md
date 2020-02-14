# [环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode* head) {
        ListNode* walker = head;
        ListNode* runner = head;
        while(runner && runner->next){
            walker = walker->next;
            runner = runner->next->next;
            if(runner == walker)
                break;
        }
        if(!runner || !runner->next)
            return nullptr;
        ListNode* headWalker = head;
        ListNode* crossWalker = walker;
        while(headWalker != crossWalker){
            headWalker = headWalker->next;
            crossWalker = crossWalker->next;
        }
        return headWalker;
    }
};
```



参考资料：[每天一道LeetCode-----判断链表是否有环，如果有，找到环的入口位置](https://blog.csdn.net/sinat_35261315/article/details/79205157)