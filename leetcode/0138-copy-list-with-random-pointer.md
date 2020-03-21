# [复制带随机指针的链表](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

### 方法一

哈希表

```java
class Solution {
    public Node copyRandomList(Node head) {
        Map<Node, Node> map = new HashMap<>();
        Node p = head;
        while (p != null) {
            map.put(p, new Node(p.val));
            p = p.next;
        }
        p = head;
        while (p != null) {
            map.get(p).next = map.get(p.next);
            map.get(p).random = map.get(p.random);
            p = p.next;
        }
        return map.get(head);
    }
}
```

### 方法二

三步走

```java
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;
        // 复制节点
        Node node = head;
        while (node != null) {
            Node tmp = new Node(node.val);
            tmp.next = node.next;
            node.next = tmp;
            node = tmp.next;
        }
        // 复制random指针
        node = head;
        while (node != null) {
            if (node.random != null) {
                node.next.random = node.random.next;
            }
            node = node.next.next;
        }
        // 节点拆分
        node = head;
        Node tmp = head.next;
        Node res = head.next;
        while (node != null) {
            node.next = node.next.next;
            if (tmp.next != null) {
                tmp.next = tmp.next.next;
            }
            node = node.next;
            tmp = tmp.next;
        }
        return res;
    }
}
```