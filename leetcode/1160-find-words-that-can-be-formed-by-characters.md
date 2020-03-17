# [拼写单词](https://leetcode-cn.com/problems/find-words-that-can-be-formed-by-characters/)

```java
class Solution {
    public int countCharacters(String[] words, String chars) {
        int res = 0;
        int[] letterMap = countLetters(chars);
        for (String word : words) {
            int[] wordMap = countLetters(word);
            for (int i = 0; i < 26; i++) {
                if (wordMap[i] > letterMap[i]) {
                    break;
                }
                if (i == 25) {
                    res += word.length();
                }
            }
        }
        return res;
    }

    private int[] countLetters(String str) {
        int[] map = new int[26];
        for (char c : str.toCharArray()) {
            map[(int)(c - 'a')] += 1;
        }
        return map;
    }
}
```

