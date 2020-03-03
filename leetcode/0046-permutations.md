# [全排列](https://leetcode-cn.com/problems/permutations/)

### 普通版

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        int len = nums.length;
        List<List<Integer>> res = new ArrayList<>();
        if(len == 0)
            return res;
        boolean[] used = new boolean[len];
        List<Integer> path = new ArrayList<>();
        dfs(nums, len, 0, path, used, res);
        return res;
    }

    private void dfs(int nums[], int len, int depth,List<Integer> path, 
                    boolean[] used, List<List<Integer>> res){
        if(depth == len){
            res.add(new ArrayList<>(path));
            return;
        }
        for(int i = 0; i < len; i++){
            if(!used[i]){
                path.add(nums[i]);
                used[i] = true;
                dfs(nums, len, depth+1, path, used, res);
                used[i] = false;
                path.remove(depth);
            }
        }                   
    }
}
```

### 改良版

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        int len = nums.length;
        //初始化ArrayList长度
        List<List<Integer>> res = new ArrayList<>(factorial(len));
        if(len == 0)
            return res;
        //哈希表降低复杂度
        Set<Integer> used = new HashSet<>(len);
        //改用栈
        Deque<Integer> path = new ArrayDeque<>(len);
        dfs(nums, len, 0, path, used, res);
        return res;
    }

     private int factorial(int n) {
        int res = 1;
        for (int i = 2; i <= n; i++) {
            res *= i;
        }
        return res;
    }

    private void dfs(int nums[], int len, int depth,Deque<Integer> path, 
                    Set<Integer> used, List<List<Integer>> res){
        if(depth == len){
            res.add(new ArrayList<>(path));
            return;
        }
        for(int i = 0; i < len; i++){
            if(!used.contains(i)){
                used.add(i);
                path.addLast(nums[i]);
                dfs(nums, len, depth + 1, path, used, res);
                path.removeLast();
                used.remove(i);
            }
        }                   
    }
}
```

