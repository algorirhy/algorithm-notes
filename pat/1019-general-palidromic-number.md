# [General Palindromic Number](https://pintia.cn/problem-sets/994805342720868352/problems/994805487143337984)

```c++
#include <cstdio>

bool Judege(int z[], int num){
    for(int i = 0; i <= num/2; i++){
        if(z[i] != z[num-1-i]) return false;
    }
    return true;
}

int main(){
    int n, b, z[40], num = 0;
    scanf("%d%d", &n, &b);
    do{
        z[num++] = n % b;
        n /= b;
    }while(n != 0);
    if(Judege(z, num)) printf("Yes\n");
    else printf("No\n");
    for(int i = num-1; i >= 0; i--){
        printf("%d", z[i]);
        if(i) printf(" ");
    }
    return 0;
}
```

