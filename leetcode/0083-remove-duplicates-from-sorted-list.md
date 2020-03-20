# [删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        ListNode preHead = new ListNode(0);
        preHead.next = head;
        ListNode pre = preHead;
        ListNode end = head;
        while (end != null) {
            if (end.next != null && end.val == end.next.val) {
                while (end.next != null && end.val == end.next.val) {
                    end = end.next;
                }
                pre.next = end;
            }
            pre = pre.next;
            end = end.next;      
        }
        return preHead.next;
    }
}
```

