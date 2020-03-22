# [第N个数字](https://leetcode-cn.com/problems/nth-digit/)

```java
class Solution {
    public int findNthDigit(int n) {
        //总位数
        int sum_th = 0;
        //数字位数 一位 两位 三位
        int i = 1;
        //当前数值
        int k = 0;
        while(sum_th < n){
            //防止溢出
            if(sum_th + i * 9 * Math.pow(10, i - 1) >= n){
                break;
            }
            k += 9 * Math.pow(10, i - 1);
            sum_th += i * 9 * Math.pow(10, i - 1);
            i++;
        }
        //剩余数字个数
        int temp = (n - sum_th) / i;
        int mod = (n - sum_th) % i;
        k += temp;
        if(mod == 0){
            return k % 10;
        }else{
            k++;
            return String.valueOf(k).charAt(mod - 1)-'0';
        }
    }
}
```

