# [山脉数组中查找目标值](https://leetcode-cn.com/problems/find-in-mountain-array/)

二分查找

```java
class Solution {
    public int findInMountainArray(int target, MountainArray mArr) {
        int peak_idx = peakIndex(mArr);
        int res = bSearch(target, mArr, 0, peak_idx, true);
        return res >= 0 ? res : bSearch(target, mArr, peak_idx, mArr.length() - 1, false);
    }

    private int peakIndex(MountainArray mArr) {
        int low = 0, high = mArr.length() - 1;
        while (low < high) {
            int mid = low + (high - low) / 2;
            if (mid == 0) return 1;
            if (mid == mArr.length() - 1) return mArr.length() - 2;
            Integer mid_val = mArr.get(mid),
                    left_val = mArr.get(mid - 1),
                    right_val = mArr.get(mid + 1);
            if (mid_val > left_val && mid_val > right_val) return mid;
            if (left_val - mid_val > 0) high = mid - 1;
            else low = mid + 1;
        }
        return low;
    }

    private int bSearch(int target, MountainArray mArr, int begin, int end, boolean mode) {
        while (begin < end) {
            int mid = begin + (end - begin) / 2;
            Integer mid_val = mArr.get(mid);
            if (mid_val == target) return mid;
            if (mid_val > target == mode) end = mid - 1;
            else begin = mid + 1;
        }
        return mArr.get(begin) == target ? begin : -1;
    }
}
```

