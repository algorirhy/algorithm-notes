# [单调数列](https://leetcode-cn.com/problems/monotonic-array/)

一次遍历

```go
func isMonotonic(A []int) bool {
    inc, dec := true, true
    for i := 0; i < len(A)-1; i++ {
        if A[i] > A[i+1] {
            inc = false
        }
        if A[i] < A[i+1] {
            dec = false
        }
    }
    return inc || dec
}
```
