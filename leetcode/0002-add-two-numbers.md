# [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

```C++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummyNode = new ListNode(0);
        ListNode* p = l1;
        ListNode* q = l2;
        ListNode* curr = dummyNode;
        int carry = 0;
        while(p || q){
            int x = (p) ? p->val : 0;
            int y = (q) ? q->val : 0;
            int sum = x + y + carry;
            carry = sum / 10;
            curr->next = new ListNode(sum%10);
            curr = curr->next;
            if(p!=NULL) p = p->next;
            if(q!=NULL) q = q->next;
        }
        if(carry) curr->next = new ListNode(carry);
        return dummyNode->next;
    }
};
```

