# [将数组分成和相等的三个部分](https://leetcode-cn.com/problems/partition-array-into-three-parts-with-equal-sum/)

### 方法一

双指针

```java
class Solution {
    public boolean canThreePartsEqualSum(int[] A) {
        int sum = 0;
        for (int num : A) {
            sum += num;
        }
        if (sum % 3 > 0) return false;
        int left = 0, right = A.length - 1;
        int leftSum = A[left], rightSum = A[right];
        while (left + 1 < right) {
            if (leftSum == sum / 3 && rightSum == sum / 3) {
                return true;
            }
            if (leftSum != sum / 3) {
                leftSum += A[++left];
            }
            if (rightSum != sum / 3) {
                rightSum += A[--right];
            }
        }
        return false;
    }
}
```

### 方法二

直接找

```java
class Solution {
    public boolean canThreePartsEqualSum(int[] A) {
        int sum = 0;
        for (int num : A) {
            sum += num;
        }
        if (sum % 3 > 0) return false;
        int s = 0;
        int flag = 0;
        for (int num : A) {
            s += num;
            if (s == sum / 3) {
                flag++;
                s = 0;
            }
        }
        return flag >= 3;
    }
}
```

