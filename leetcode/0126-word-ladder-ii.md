# [单词接龙 II](https://leetcode-cn.com/problems/word-ladder-ii)

BFS

```java
class Solution {
    public List<List<String>> findLadders(String begin, String end, List words) {
        List<List<String>> res = new ArrayList<>();
        // 如果不含有结束单词，直接结束，不然后边会造成死循环
        if (!words.contains(end)) {
            return res;
        }
        bfs(begin, end, words, res);
        return res;
    }

    private void bfs(String begin, String end, List words, List res) {
        Deque<List<String>> queue = new ArrayDeque<>();
        List<String> path = new ArrayList<>();
        path.add(begin);
        queue.offer(path);
        boolean isFound = false;
        Set<String> dict = new HashSet<>(words);
        Set<String> visited = new HashSet<>();
        visited.add(begin);
        while (!queue.isEmpty()) {
            int size = queue.size();
            Set<String> subVisited = new HashSet<>();
            for (int j = 0; j < size; j++) {
                List<String> p = queue.poll();
                //得到当前路径的末尾单词
                String temp = p.get(p.size() - 1);
                // 一次性得到所有的下一个的节点
                ArrayList<String> neighbors = getNeighbors(temp, dict);
                for (String neighbor : neighbors) {
                    //只考虑之前没有出现过的单词
                    if (!visited.contains(neighbor)) {
                        //到达结束单词
                        if (neighbor.equals(end)) {
                            isFound = true;
                            p.add(neighbor);
                            res.add(new ArrayList<String>(p));
                            p.remove(p.size() - 1);
                        }
                        //加入当前单词
                        p.add(neighbor);
                        queue.offer(new ArrayList<String>(p));
                        p.remove(p.size() - 1);
                        subVisited.add(neighbor);
                    }
                }
            }
            visited.addAll(subVisited);
            if (isFound) {
                break;
            }
        }
    }

    private ArrayList<String> getNeighbors(String node, Set dict) {
        ArrayList<String> res = new ArrayList<String>();
        char chs[] = node.toCharArray();
        for (char ch = 'a'; ch <= 'z'; ch++) {
            for (int i = 0; i < chs.length; i++) {
                if (chs[i] == ch)
                    continue;
                char old_ch = chs[i];
                chs[i] = ch;
                if (dict.contains(String.valueOf(chs))) {
                    res.add(String.valueOf(chs));
                }
                chs[i] = old_ch;
            }

        }
        return res;
    }
}
```

