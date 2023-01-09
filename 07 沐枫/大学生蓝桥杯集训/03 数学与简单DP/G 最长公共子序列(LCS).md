### [题目详情 - 最长公共子序列(LCS) - 沐枫OJ (mfstem.org)](https://www.mfstem.org/p/550?tid=63b6b08e485e4d04afcdd0d6)
![[897. 最长公共子序列]]

#### 代码
```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1010;

int n, m;
string a, b;
int f[N][N];

int main(){
    
    cin >> a >> b;
    int n = a.size(), m = b.size();

    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= m; j++){
            f[i][j] = max(f[i - 1][j], f[i][j - 1]);
            if(a[i - 1] == b[j - 1]) f[i][j] = max(f[i][j], f[i - 1][j - 1] + 1);
        }
    }

    cout << f[n][m] << endl;

    return 0;
}
```


*2022-12-31 周六*