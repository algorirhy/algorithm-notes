# [翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string)

```C++
class Solution {
public:
    string reverseWords(string s) {
        reverse(s.begin(),s.end());
        int index = 0;
        for (int i = 0;i < s.size();i++) {
            if (s[i] != ' ') {
                if (index != 0) s[index++] = ' ';
                int j = i;
                while (j < s.size() && s[j] != ' ') s[index++] = s[j++];
                reverse(s.begin() + index - (j - i),s.begin() + index);
                i = j;
            } 
        }
        s.resize(index);
        return s;
    }
};
```

