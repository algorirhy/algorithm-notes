# [字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi) 

```c++
class Solution {
public:
    int myAtoi(string str) {
        int size = str.size(), s = 1, index = 0;
        long long res = 0;
        if(size == 0)
            return 0;
        while(str[index] == ' ')
            index++;
        if(str[index] == '-')
            s = -1;
        for(int i=(str[index] == '-' || str[index] == '+') ? index+1:index; i<size; i++){
            if(str[i] < '0' || str[i] > '9')
                break;
            res = res * 10 + (str[i]-'0');
            if(res > INT_MAX)
                break;
        }
        res *= s;
        if(res > INT_MAX){
            return INT_MAX;
        }else if(res < INT_MIN){
            return INT_MIN;
        }
        return res;
    }
};
```

