# [使数组唯一的最小增量](https://leetcode-cn.com/problems/minimum-increment-to-make-array-unique/)

### 方法一

先排序 O(nlogn)

```java
class Solution {
    public int minIncrementForUnique(int[] A) {
        Arrays.sort(A);
        int move = 0;
        for (int i = 1; i < A.length; i++) {
            if (A[i] <= A[i - 1]) {
                move += A[i - 1] - A[i] + 1;
                A[i] = A[i - 1] + 1;
            }
        }
        return move;
    }
}
```

### 方法二

计数排序 O(n)

```java
class Solution {
    public int minIncrementForUnique(int[] A) {
        int[] counter = new int[40001];
        int min = 40000, max = -1;
        for (int num : A) {
            counter[num]++;
            min = Math.min(min, num);
            max = Math.max(max, num);
        }
        int move = 0;
        for (int i = min; i <= max; i++) {
            if (counter[i] > 1) {
                int d = counter[i] - 1;
                move += d;
                counter[i + 1] += d;
            }
        }
        // 超过max的部分
        int d = counter[max + 1] - 1;
        move += (d + 1) * d / 2;
        return move;
    }
}
```

### 方法三

线性探测 O(n) 

```java
class Solution {
    int[] posMap = new int [80000];

    public int minIncrementForUnique(int[] A) {
        Arrays.fill(posMap, -1);
        int move = 0;
        for (int num: A) {
            int pos = findPos(num); 
            move += pos - num;
        }
        return move;
    }

    private int findPos(int num) {
        int pos = posMap[num];
        if (pos == -1) {
            posMap[num] = num;
            return num;
        }
        // 向后寻址
        pos = findPos(pos + 1); 
        // 路径压缩
        posMap[num] = pos; 
        return pos;
    }
}
```

