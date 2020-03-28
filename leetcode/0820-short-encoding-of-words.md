# [单词的压缩编码](https://leetcode-cn.com/problems/short-encoding-of-words/)

```java
class Solution {
    public int minimumLengthEncoding(String[] words) {
        int res = 0;
        Trie tire = new Trie();
        // 从长到短排序 atime btime 需要12个
        Arrays.sort(words, (a, b) -> b.length() - a.length());
        for (String word : words) {
            res += tire.insert(word);
        }
        return res;
    }

    class Trie {
        private TireNode root;

        public Trie() {
            root = new TireNode();
        }

        public int insert(String word) {
            // 是否是新单词
            boolean isNew = false;
            TireNode node = root;
            char[] ch = word.toCharArray();
            // 后缀插入
            for (int i = ch.length - 1; i >= 0; i--) {
                if (node.next[ch[i] - 'a'] == null) {
                    isNew = true;
                    node.next[ch[i] - 'a'] = new TireNode();
                }
                node = node.next[ch[i] - 'a'];
            }
            return isNew ? word.length() + 1 : 0;
        }
    }

    class TireNode {
        TireNode[] next;

        public TireNode() {
            next = new TireNode[26];
        }
    }
}
```

