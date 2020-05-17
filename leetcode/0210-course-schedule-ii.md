# [课程表 II](https://leetcode-cn.com/problems/course-schedule-ii/)

拓扑排序

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        if (numCourses <= 0) {
            return new int[0];
        }
        int[] inDegree = new int[numCourses];
        Set<Integer>[] adj = new HashSet[numCourses];
        for (int i = 0; i < numCourses; i++) {
            adj[i] = new HashSet<>();
        }
        for (int[] pre : prerequisites) {
            adj[pre[1]].add(pre[0]);
            inDegree[pre[0]]++;
        }
        Queue<Integer> queue = new ArrayDeque<>();
        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] == 0) {
                queue.offer(i);
            }
        }
        int count = 0;
        int[] res = new int[numCourses];
        while (!queue.isEmpty()) {
            Integer head = queue.poll();
            res[count++] = head;
            for (Integer nextCourse : adj[head]) {
                inDegree[nextCourse]--;
                if (inDegree[nextCourse] == 0) {
                    queue.offer(nextCourse);
                }
            }
        }
        if (count == numCourses) {
            return res;
        }
        return new int[0];
    }
}
```

