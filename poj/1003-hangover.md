# [Hangover](http://bailian.openjudge.cn/practice/1003/)

```C++
#include <iostream>

using namespace std;

int main() {
    float length;
    while (cin >> length && length != 0.00) {
        int i;
        float sum = 0;
        for (i = 2;; i++) {
            sum += 1.0 / i;
            if (sum > length) {
                cout << i - 1 << " card(s)" << endl;
                break;
            }
        }
    }
    return 0;
}
```

