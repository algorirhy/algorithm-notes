# [罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer)

```C++
class Solution {
public:
    int romanToInt(string s) {
        int l=s.length();
        int now=0,ans=0;  
        for(int i=0; i<l; i++){
            if(s[i]=='I') {
                now = 1;
                if(i+1<l&&s[i+1]=='V'){ now=4; i++; }
                else if(i+1<l&&s[i+1]=='X'){ now=9; i++; }  
            }
            else if(s[i]=='X') {
                now = 10;
                if(i+1<l&&s[i+1]=='L'){ now = 40; i++; }
                else if(i+1<l&&s[i+1]=='C'){ now=90; i++; }
            }
            else if(s[i]=='C') {
                now = 100;
                if(i+1<l&&s[i+1]=='D') { now=400; i++; }
                else if(i+1<l&&s[i+1]=='M') { now=900; i++; }
            }
            else if(s[i]=='V') { now=5; }  
            else if(s[i]=='L') { now=50; }  
            else if(s[i]=='D') { now=500; }  
            else if(s[i]=='M') { now=1000; }  
            
            ans+=now;  
        }
        return ans;
    }
};
```

