# [两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs)

### 方法一

递归

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode next = head.next;
        head.next = swapPairs(next.next);
        next.next = head;
        return next;
    }
}
```

### 方法二

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode preHead = new ListNode(-1);
        preHead.next = head;
        ListNode cur = preHead;
        while (cur.next != null && cur.next.next != null) {
            ListNode pre  = cur.next;
            ListNode next = pre.next;

            cur.next = next;
            pre.next = next.next;
            next.next = pre;
            cur = pre;
        }
        return preHead.next;
    }
}
```

