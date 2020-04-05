# [LFU缓存](https://leetcode-cn.com/problems/lfu-cache/)

```java
class LFUCache {
    // key 及对应的节点（包括 value 和频率）
    Map<Integer, Node> cache;
    // 频率及对应的双向链表
    Map<Integer, LinkedHashSet<Node>> freqMap;
    int min;
    int size;
    int capacity;

    public LFUCache(int capacity) {
        this.capacity = capacity;
        cache = new HashMap<>(capacity);
        freqMap = new HashMap<>();
    }
    
    public int get(int key) {
        Node node = cache.get(key);
        if (node == null) {
            return -1;
        }
        updateFreq(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        if (capacity == 0) return;
        Node node = cache.get(key);
        if (node != null) {
            // 原来存在该节点
            node.value = value;
            updateFreq(node);
        } else {
            if (size == capacity) {
                Node deadNode = removeNode();
                cache.remove(deadNode.key);
                size--;
            }
            Node newNode = new Node(key, value);
            cache.put(key, newNode);
            addNode(newNode);
            size++;     
        }
    }
	
    // 更新频率
    private void updateFreq(Node node) {
        // 从原freq对应的链表里移除, 并更新min
        int freq = node.freq;
        LinkedHashSet<Node> freqList = freqMap.get(freq);
        freqList.remove(node);
        if (freq == min && freqList.size() == 0) { 
            min = freq + 1;
        }
        // 加入新freq对应的链表
        node.freq++;
        LinkedHashSet<Node> newfreqList = freqMap.get(freq + 1);
        if (newfreqList == null) {
            newfreqList = new LinkedHashSet<>();
            freqMap.put(freq + 1, newfreqList);
        }
        newfreqList.add(node);
    }
	
    private void addNode(Node node) {
        // 找到频率为 1 的链表
        LinkedHashSet<Node> freqList = freqMap.get(1);
        if (freqList == null) {
            freqList = new LinkedHashSet<>();
            freqMap.put(1, freqList);
        } 
        // 添加到链表末尾
        freqList.add(node); 
        min = 1;
    }
	
    private Node removeNode() {
        // 找到频率最低的链表
        LinkedHashSet<Node> freqList = freqMap.get(min);
        // 找到链表的第一个节点（最近最少使用的节点）
        Node deadNode = freqList.iterator().next();
        freqList.remove(deadNode);
        return deadNode;
    }
}

class Node {
    int key, value;
    int freq = 1;

    public Node (int key, int value) {
        this.key = key;
        this.value = value;
    }
}
```

