# [查找和最小的 K 对数字](https://leetcode-cn.com/problems/find-k-pairs-with-smallest-sums/)

### 优先队列

```Go
func kSmallestPairs(nums1 []int, nums2 []int, k int) [][]int {
    n, m, ans := len(nums1), len(nums2), [][]int{}
    flag := n > m
    if flag {
        n, m, nums1, nums2 = m, n, nums2, nums1
    }
    if n > k {
        n = k
    }
    pq := make(hp, n)
    for i := 0; i < n; i++ {
        pq[i] = []int{nums1[i] + nums2[0], i, 0}
    }
    heap.Init(&pq)
    for pq.Len() > 0 && len(ans) < k {
        poll := heap.Pop(&pq).([]int)
        a, b := poll[1], poll[2]
        if flag {
            ans = append(ans, []int{nums2[b], nums1[a]})
        } else {
            ans = append(ans, []int{nums1[a], nums2[b]})
        }
        if b < m - 1 {
            heap.Push(&pq, []int{nums1[a] + nums2[b +1], a, b + 1})
        }
    }
    return ans
}

type hp [][]int
func (h hp) Len() int {return len(h)}
func (h hp) Less(i, j int) bool {return h[i][0] < h[j][0]}
func (h hp) Swap(i, j int) {h[i], h[j] = h[j], h[i]}
func (h *hp) Push(v interface{}) {*h = append(*h, v.([]int))}
func (h *hp) Pop() interface{} {tmp := *h; v := tmp[len(tmp)-1]; *h = tmp[:len(tmp)-1]; return v}
```

