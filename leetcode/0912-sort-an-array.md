# [排序数组](https://leetcode-cn.com/problems/sort-an-array/)

### 冒泡排序（超时）

```java
    public void bubbleSort(int[] arr) {
        int len = arr.length;
        for (int i = 0; i < len; i++) {
            boolean isSwap = false;
            for (int j = 0; j < len - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // 大于后一个数，交换
                    swap(arr, j, j + 1);
                    isSwap = true;
                }
            }
            // 未交换， 退出排序
            if (!isSwap) {
                break;
            }
        }
    }

    private void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
```

### 插入排序

```java
    public void insertionSort(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            int tmp = arr[i];
            int pos = i;
            while (pos > 0 && arr[pos - 1] > tmp) {
                arr[pos] = arr[pos - 1];
                pos--;
            }
            arr[pos] = tmp;
        }
    }
```

### 希尔排序

```java
    public void shellSort(int[] arr) {
        int len = arr.length;
        for (int step = len / 2; step >= 1; step /= 2) {
            for (int i = 0; i < step; i++) {
                // 插入排序
                for (int j = i + step; j < len; j += step) {
                    int tmp = arr[j];
                    int pos = j;
                    while (pos >= step && arr[pos - step] > tmp) {
                        arr[pos] = arr[pos - step];
                        pos -= step;
                    }
                    arr[pos] = tmp;
                }
            }
        }
    }
```

### 选择排序

```java
    public void selectionSort(int[] arr) {
        int len = arr.length;
        for (int i = 0; i < len; i++) {
            int min = i;
            for (int j = i + 1; j < len; j++) {
                if (arr[j] < arr[min]) {
                    min = j;
                }
            }
            swap(arr, min, i);
        }
    }

    private void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
```

### 归并排序

```java
    public void mergeSort(int[] arr) {
        int len = arr.length;
        int[] tmp = new int[len];
        mSort(arr, tmp, 0, len - 1);
    }

    private void mSort(int[] arr, int[] tmp, int startIndex, int endIndex) {
        if (endIndex <= startIndex) {
            return;
        }
        int midIndex = startIndex + (endIndex - startIndex) / 2;
        mSort(arr, tmp, startIndex, midIndex);
        mSort(arr, tmp, midIndex + 1, endIndex);
        merge(arr, tmp, startIndex, midIndex, endIndex);
    }

    private void merge(int[] arr, int[] tmp, int startIndex, int midIndex, int endIndex){
        System.arraycopy(arr, startIndex, tmp, startIndex, endIndex + 1 - startIndex);
        int left = startIndex;
        int right = midIndex + 1;
        for (int i = startIndex; i <= endIndex; i++) {
            if (left > midIndex) {
                // 左边的数据已经排完
                arr[i] = tmp[right++];
            } else if (right > endIndex) {
                // 右边的数据已经排完
                arr[i] = tmp[left++];
            } else if (tmp[left] < arr[right]) {
                arr[i] = tmp[left++];
            } else {
                arr[i] = tmp[right++];
            }
        }
    }
```

### 快速排序

```java
    public void quickSort(int[] arr) {
        qSort(arr, 0, arr.length - 1);
    }

    private void qSort(int[] arr, int low, int high) {
        if (low >= high) {
            return;
        }
        int pos = partition(arr, low, high);
        qSort(arr, low, pos - 1);
        qSort(arr, pos + 1, high);
    }

    private int partition(int[] arr, int low, int high) {
        // 可使用三数取中法/随机法优化
        int pivot = arr[low];
        while (low < high) {
            while (low < high && arr[high] > pivot) {
                high--;
            }
            arr[low] = arr[high];
            while (low < high && arr[low] <= pivot) {
                low++;
            }
            arr[high] = arr[low];
        }
        arr[low] = pivot;
        return low;
    }
```

### 基数排序

```java
    public void radixSort(int[] arr) {
        int min = arr[0], max = arr[0];
        for (int num : arr) {
            min = Math.min(min, num);
            max = Math.max(max, num);
        }
        // 求得绝对值最大的值
        max = Math.max(max, -min);
        // 当前排序位置
        int digits = 0;
        // 计算 max 的位数
        while (max > 0) {
            max /= 10;
            digits++;
        }
        // 考虑负数 桶的数量
        int bucketNum = 19;
        ArrayList<ArrayList<Integer>> bucketList = new ArrayList<>(bucketNum);
        for (int i = 0; i < bucketNum; i++) {
            bucketList.add(new ArrayList<>());
        }
        for (int i = 0, mod = 1; i < digits; i++, mod *= 10) {
            for (int num : arr) {
                // 计算余数 放入相应的桶
                int pos = (num / mod) % 10;
                bucketList.get(pos + 9).add(num);
            }
            // 写回数组
            int index = 0;
            for (ArrayList<Integer> bucket : bucketList) {
                for (int num : bucket) {
                    arr[index++] = num;
                }
                bucket.clear();
            }
        }
    }
```

### 计数排序

```java
    public void countingSort(int[] arr) {
        int max = arr[0];
        int min = arr[0];
        for (int num : arr) {
            min = Math.min(min, num);
            max = Math.max(max, num);
        }
        int[] counter = new int[max - min + 1];
        for (int num : arr) {
            counter[num - min]++;
        }
        int index = 0;
        for (int i = 0; i < max - min + 1; i++) {
            while (counter[i] > 0) {
                arr[index++] = i + min;
                counter[i]--;
            }
        }
    }
```

### 桶排序

```java
    public void bucketSort(int[] arr) {
        int min = arr[0], max = arr[0];
        for (int num : arr) {
            min = Math.min(min, num);
            max = Math.max(max, num);
        }
        // 桶的区间大小
        int interval = 10;
        // 桶的数量
        int bucketNum = (max - min) / interval + 1;
        ArrayList<ArrayList<Integer>> bucketList = new ArrayList<>();
        for (int i = 0; i < bucketNum; i++) {
            bucketList.add(new ArrayList<>());
        }
        // 把所有元素放入对应的桶里面
        for (int num : arr) {
            int pos = (num - min) / interval;
            bucketList.get(pos).add(num);
        }
        // 桶内排序
        for (ArrayList<Integer> list : bucketList) {
            Collections.sort(list);
        }
        // 写入原数组
        int index = 0;
        for (ArrayList<Integer> list : bucketList) {
            for (int num : list) {
                arr[index] = num;
                index++;
            }
        }
    }
```

### 堆排序

```java
    public void heapSort(int[] arr) {
        int len = arr.length;
        buildHeap(arr, len);
        for (int i = len - 1; i > 0; i--) {
            // 将堆顶元素与末位元素调换
            swap(arr, 0, i);
            len--;
            // 调整大顶堆
            sink(arr, 0, len);
        }
    }

    /**
     * 构建大顶堆
     *
     * @param arr 数组
     * @param len 数组长度
     */
    private void buildHeap(int[] arr, int len) {
        for (int i = len / 2; i >= 0; i--) {
            sink(arr, i, len);
        }
    }

    /**
     * 下沉调整
     *
     * @param arr   数组
     * @param index 调整的位置
     * @param len   数组长度
     */
    private void sink(int[] arr, int index, int len) {
        int parent = index;
        int lChild = 2 * index + 1;
        int rChild = 2 * index + 2;

        if (lChild < len && arr[lChild] > arr[parent]) {
            parent = lChild;
        }

        if (rChild < len && arr[rChild] > arr[parent]) {
            parent = rChild;
        }

        if (parent != index) {
            swap(arr, index, parent);
            // 继续调整
            sink(arr, parent, len);
        }
    }

    private void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
```

