# [转换成小写字母](https://leetcode-cn.com/problems/to-lower-case/)

```C++
class Solution {
public:
    string toLowerCase(string str) {
        for(int i=0; i< str.size(); i++){
            if(str[i]>='A'&&str[i]<='Z'){
                str[i]+=32;
            }
        }
        return str;
    }
};
```

