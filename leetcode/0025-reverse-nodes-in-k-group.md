# [K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group)

### 方法一

递归

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null) return null;
        // [begin, end) 前开后闭
        ListNode begin = head;
        ListNode end = head;
        for (int i = 0; i < k; i++) {
            // 元素小于 k, 直接返回head
            if (end == null) return head;
            end = end.next;
        }
        // 反转前 k 个元素
        ListNode newHead = reverse(begin, end);
        // 反转后续链表并连接起来
        begin.next = reverseKGroup(end, k);
        return newHead;
    }

    private ListNode reverse(ListNode begin, ListNode end) {
        ListNode p1 = begin;
        ListNode p2 = p1.next;
        ListNode p3 = null;
        // 注意条件 [begin, end)
        while (p2 != end) {
            p3 = p2.next;
            p2.next = p1;
            p1 = p2;
            p2 = p3;
        }
        return p1;
    }
}
```

### 方法二



```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null) return null;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        ListNode end = pre;
        while (true) {
            for (int i = 0; i < k && end != null; i++) {
                end = end.next;
            }
            if (end == null) break;
            // pre->[begin, end]->next;
            ListNode begin = pre.next;
            ListNode next = end.next;
            end.next = null;
            pre.next = reverse(begin);
            begin.next = next;
            // 重置 pre, end;
            pre = begin;
            end = pre;
        }
        return dummy.next;
    }

    // 反转链表
    private ListNode reverse(ListNode head) {
        ListNode p1 = head;
        ListNode p2 = p1.next;
        ListNode p3 = null;
        while (p2 != null) {
            p3 = p2.next;
            p2.next = p1;
            p1 = p2;
            p2 = p3;
        }
        return p1;
    }
}
```

