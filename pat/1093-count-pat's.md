# [Count PAT's](https://pintia.cn/problem-sets/994805342720868352/problems/994805373582557184)

```c++
#include <stdio.h>
#include <cstring>
#include <iostream>

using namespace std;

const int MAXN = 100010;
const int MOD = 1000000007;
char str[MAXN];
int leftNumP[MAXN] = {0};

int main(){
    cin.getline(str, MAXN);
    int len = strlen(str);
    for(int i = 0; i < len; i++){
        if(i > 0){
            leftNumP[i] = leftNumP[i-1];
        }
        if(str[i] == 'P'){
            leftNumP[i]++;
        }
    }
    int ans = 0, rightNumT = 0;
    for(int i = len - 1; i >= 0; i--){
        if(str[i] == 'T'){
            rightNumT++;
        }else if(str[i] == 'A'){
            ans = (ans + leftNumP[i] * rightNumT) % MOD;
        }
    }
    printf("%d\n", ans);
    return 0;
}
```

