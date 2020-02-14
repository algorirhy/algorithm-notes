# [环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

使用快慢指针

```c++
class Solution {
public:
    bool hasCycle(ListNode* head) {
        ListNode* walker = head;
        ListNode* runner = head;

        while(runner && runner->next){
            walker = walker->next;
            runner = runner->next->next;
            if(walker == runner)
                return true;
        }
        return false;
    }
};
```



参考资料：[每天一道LeetCode-----判断链表是否有环，如果有，找到环的入口位置](https://blog.csdn.net/sinat_35261315/article/details/79205157)

