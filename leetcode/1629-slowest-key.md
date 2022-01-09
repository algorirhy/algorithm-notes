# [按键持续时间最长的键](https://leetcode-cn.com/problems/slowest-key/)

```go
func slowestKey(releaseTimes []int, keysPressed string) byte {
    ans := keysPressed[0]
    maxTime := releaseTimes[0]
    for i:=1; i < len(keysPressed); i++{
        pressTime := releaseTimes[i] - releaseTimes[i-1]
        if pressTime > maxTime || (pressTime == maxTime && keysPressed[i] > ans) {
            ans = keysPressed[i]
            maxTime = pressTime
        }
    }
    return ans
}
```

