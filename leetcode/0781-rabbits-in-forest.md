# [森林中的兔子](https://leetcode-cn.com/problems/rabbits-in-forest/)

贪心算法

```Go
func numRabbits(answers []int) (ans int) {
    count := map[int]int{}
    for _, v := range answers {
        count[v]++
    }
    for x, y := range count {
        ans += (x + y) / (x + 1) * (x + 1)
    }
    return
}
```
