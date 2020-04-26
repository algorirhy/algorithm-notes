# [合并K个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        ListNode preHead = new ListNode(-1);
        ListNode preNode = preHead;
        PriorityQueue<ListNode> pq = new PriorityQueue<>(new Comparator<ListNode>() {
            @Override
            public int compare(ListNode n1, ListNode n2) {
                return n1.val - n2.val;
            }
        });
        for (ListNode node : lists) {
            if (node != null) {
                pq.offer(node);
            }
        }
        while(!pq.isEmpty()) {
            ListNode min = pq.poll();
            preNode.next = min;
            if (min.next != null) {
                pq.offer(min.next);
            }
            preNode = preNode.next;
        }
        return preHead.next;
    }
}
```

