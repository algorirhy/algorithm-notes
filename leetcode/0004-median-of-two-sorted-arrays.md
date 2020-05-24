# [寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

二分查找

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int m = nums2.length;
        int left = (n + m + 1) / 2;
        int right = (n + m ) / 2 + 1;
        int leftNum = getKth(nums1, 0, n - 1, nums2, 0, m - 1, left);
        int rightNum = getKth(nums1, 0, n - 1, nums2, 0, m - 1, right);
        return (leftNum + rightNum) * 0.5;
    }

    private int getKth(int[] nums1, int begin1, int end1, int[] nums2, int begin2, int end2, int k) {
        int len1 = end1 - begin1 + 1;
        int len2 = end2 - begin2 + 1;
        // 让 len1 的长度小于 len2，这样就能保证如果有数组空了，一定是 len1 
        if (len1 > len2) return getKth(nums2, begin2, end2, nums1, begin1, end1, k);
        if (len1 == 0) return nums2[begin2 + k - 1];
        if (k == 1) return Math.min(nums1[begin1], nums2[begin2]);
        int i = begin1 + Math.min(len1, k / 2) - 1;
        int j = begin2 + Math.min(len2, k / 2) - 1;
        if (nums1[i] > nums2[j]) {
            return getKth(nums1, begin1, end1, nums2, j + 1, end2, k - (j - begin2 + 1));
        } else {
            return getKth(nums1, i + 1, end1, nums2, begin2, end2, k - (i - begin1 + 1));
        }
    }
}
```

