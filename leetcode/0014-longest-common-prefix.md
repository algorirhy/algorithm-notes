# [最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)

## C++

```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size() == 0)
            return "";
        string res = strs[0];
        for(int i = 1; i < strs.size(); i++){
            while(strs[i].find(res) != 0){
                if (res == "") 
                    return "";
                res = res.substr(0, res.length() - 1);
            }
        }
        return res;
    }
};
```



## Java

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0)
            return "";
        String res = strs[0];
        for(int i = 1; i < strs.length; i++){
            while(strs[i].indexOf(res) != 0){
                if(res == "")
                    return "";
                res = res.substring(0, res.length() - 1);
            }
        }
        return res;
    }
}
```

