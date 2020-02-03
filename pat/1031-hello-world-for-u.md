# [Hello World for U](https://pintia.cn/problem-sets/994805342720868352/problems/994805462535356416)

```c++
#include <cstdio>
#include <cstring>
#include <iostream>

using namespace std;

int main(){
    char str[100], ans[40][40];
    cin.getline(str,100);
    int N = strlen(str);
    int n1 = (N + 2) / 3, n3 = n1, n2 = N + 2 - n1 - n3;
    for(int i = 1; i <= n1; i++){
        for(int j = 1; j <= n2; j++){
            ans[i][j] = ' ';
        }
    }
    int pos = 0;
    for(int i = 1; i<= n1; i++){
        ans[i][1] = str[pos++];
    }
    for(int j = 2; j <= n2; j++){
        ans[n1][j] = str[pos++];
    }
    for(int i = n3 - 1; i >= 1; i--){
        ans[i][n2] = str[pos++];
    }
    for(int i = 1; i <= n1; i++){
        for(int j = 1; j <= n2; j++){
            printf("%c", ans[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

