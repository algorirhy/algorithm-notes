# [环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode walker = head;
        ListNode runner = head;
        while (runner != null && runner.next != null) {
            walker = walker.next;
            runner = runner.next.next;
            if (walker == runner) break;
        }
        if (runner == null || runner.next == null) return null;
        ListNode headWalker = head;
        ListNode crossWalker = walker;
        while (headWalker != crossWalker) {
            headWalker = headWalker.next;
            crossWalker = crossWalker.next;
        }
        return headWalker;
    }
}
```

