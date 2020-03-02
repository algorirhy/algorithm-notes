# [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

### 递归

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head || !head->next)
            return head;
        ListNode* new_head = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return new_head;
    }
};
```

### 非递归

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head || !head->next)
            return head;
        ListNode* p1 = head;
        ListNode* p2 = p1->next;
        ListNode* p3;
        while(p2){
            p3 = p2->next;
            p2->next = p1;
            p1 = p2;
            p2 = p3;
        }
        head->next = nullptr;
        return p1;
    }
};
```

