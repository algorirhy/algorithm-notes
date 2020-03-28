# [LRU缓存机制](https://leetcode-cn.com/problems/lru-cache/)

### 方法一

哈希表 + 双向链表

```java
class LRUCache {

    // 双向链表节点
    class Node {
        public int key, val;
        public Node pre, next;
        public Node(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }

    // 双向链表
    class DoubleList {
        private Node head, tail;
        private int size;

        public DoubleList() {
            head = new Node(0, 0);
            tail = new Node(0, 0);
            head.next = tail;
            tail.pre = head;
            size = 0;
        }

        // 在链表头部添加节点 node
        public void addFirst(Node node) {
            node.pre = head;
            node.next = head.next;
            head.next.pre = node;
            head.next = node;
            size++;
        }

        // 删除链表中的 node 节点（node 一定存在）
        public void remove(Node node) {
            node.pre.next = node.next;
            node.next.pre = node.pre;
            size--;
        }

        // 删除链表中最后一个节点，并返回该节点
        public Node removeLast() {
            if (head.next == tail) return null;
            Node last = tail.pre;
            remove(last);
            return last;
        }

        // 返回链表长度
        public int size() {
            return size;
        }
    }

    private int cap;
    private DoubleList cache;
    private Map<Integer, Node> map;

    public LRUCache(int capacity) {
        cap = capacity;
        cache = new DoubleList();
        map = new HashMap<>();
    }
    
    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }
        int val = map.get(key).val;
        // 利用 put 方法把该数据提前
        put(key, val);
        return val;
    }
    
    public void put(int key, int value) {
        Node node = new Node(key, value);
        if (map.containsKey(key)) {
            // 删除原节点
            cache.remove(map.get(key));
        } else if (cache.size() == cap){
            // 容量已满，删除尾节点
            Node last = cache.removeLast();
            map.remove(last.key);
        }
        // 添加新节点
        cache.addFirst(node);
        map.put(key, node);
    }
}
```

### 方法二

利用 `LinkedHashMap`

```java
class LRUCache extends LinkedHashMap<Integer, Integer>{
    private int capacity;

    public LRUCache(int capacity) {
        //容量 加载因子 是否按读取顺序排序
        super(capacity, 0.75F, true);
        this.capacity = capacity;
    }
    
    public int get(int key) {
        return super.getOrDefault(key, -1);
    }
    
    //已继承父类的put函数，可不写。
    public void put(int key, int value) {
        super.put(key, value);
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
        return size() > capacity; 
    }
}
```
