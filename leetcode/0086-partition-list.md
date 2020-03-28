# [分隔链表](https://leetcode-cn.com/problems/partition-list/)

```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode beforeX = new ListNode(-1);
        ListNode afterX = new ListNode(-1);
        ListNode p1 = beforeX, p2 = afterX;
        while (head != null) {
            if (head.val < x) {
                p1.next = head;
                p1 = p1.next;
            } else {
                p2.next = head;
                p2 = p2.next;
            }
            head = head.next;
        }
        p1.next = afterX.next;
        p2.next = null;
        return beforeX.next;
    }
}
```

