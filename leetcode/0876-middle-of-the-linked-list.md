# [链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)

快慢指针

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        if (head == null) return null;
        ListNode fast = head;
        ListNode slow = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

