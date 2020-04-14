# [两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Deque<Integer> s1 = new ArrayDeque<>();
        Deque<Integer> s2 = new ArrayDeque<>();
        while (l1 != null) {
            s1.push(l1.val);
            l1 = l1.next;
        }
        while (l2 != null) {
            s2.push(l2.val);
            l2= l2.next;
        }
        int carry = 0;
        ListNode res = null;
        while (!s1.isEmpty() || !s2.isEmpty() || carry > 0) {
            int sum = carry;
            sum += s1.isEmpty() ? 0 : s1.pop();
            sum += s2.isEmpty() ? 0 : s2.pop();
            ListNode node = new ListNode(sum % 10);
            node.next = res;
            res = node;
            carry = sum / 10;
        }
        return res;
    }
}
```

