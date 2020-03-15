# [前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

### 方法一

最小堆

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap();
        for (int num : nums) {
            if (map.containsKey(num)) {
                map.put(num, map.get(num) + 1);
            } else {
                map.put(num, 1);
            }
        }
        // 用最小堆保存频率最大的k个元素
        PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>() {
            @Override
            public int compare(Integer a, Integer b) {
                return map.get(a) - map.get(b);
            }
        });
        for (Integer key : map.keySet()) {
            if (pq.size() < k) {
                pq.add(key);
            } else if (map.get(key) > map.get(pq.peek())) {
                pq.remove();
                pq.add(key);
            }
        }
        List<Integer> res = new ArrayList<>();
        while (!pq.isEmpty()) {
            res.add(pq.remove());
        }
        return res;
    }
}
```

### 方法二

桶排序

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        List<Integer> res = new ArrayList();
        HashMap<Integer, Integer> map = new HashMap();
        for (int num : nums) {
            if (map.containsKey(num)) {
                map.put(num, map.get(num) + 1);
            } else {
                map.put(num, 1);
            }
        }
        //桶排序：将频率作为数组下标，对于出现频率不同的数字集合，存入对应的数组下标
        List<Integer>[] buckets = new List[nums.length+1];
        for (Integer key : map.keySet()) {
            int i = map.get(key);
            if (buckets[i] == null) {
                buckets[i] = new ArrayList();
            }
            buckets[i].add(key);
        }
        for(int i = buckets.length - 1;i >= 0 && res.size() < k;i--){
            if(buckets[i] == null) continue;
            res.addAll(buckets[i]);
        }
        return res;
    }
}
```

