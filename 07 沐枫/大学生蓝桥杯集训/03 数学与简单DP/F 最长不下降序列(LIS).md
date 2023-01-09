### [题目详情 - 最长不下降序列(LIS) - 沐枫OJ (mfstem.org)](https://www.mfstem.org/p/546?tid=63b6b08e485e4d04afcdd0d6)

#DP #线性DP 

设有由 $n$ 个不相同的整数组成的数列，记为: $b_1,b_2,\dots,b_n$ 且 $b_i\neq b_j (i\neq j)$，若存在 $i_1<i_2<i_3<\dots < i_e$ 且有 $b_{i_1}<b_{i_2}<\dots <b_{i_e}$ 则称为长度为 $e$ 的不下降序列。

当原数列出之后，求出最长的不下降序列。

例如 13，7，9，16，38，24，37，18，44，19，21，22，63，15。

例中 13，16，18，19，21，22，63 就是一个长度为 7 的不下降序列，同时也有 7，9，16，18，19，21，22，63 长度为 8 的不下降序列。

#### 输入格式

输入一行若干个整数，个数小于 100，取值小于 50000。

#### 输出格式

输出两行。

第一行输出一个整数 e。

第二行输出 e 个整数，为最长不下降序列。

#### 输入样例

```in
300 250 275 252 200 138 245
```

#### 输出样例

```out
2
250 275 
```

#### 思路

求长度的思路详见: [[895. 最长上升子序列]]

#### 代码

```cpp
#include <iostream>

using namespace std;

const int N = 1e3 + 10;

int a[N], f[N];

int main(){

    int x, n = 0;
    while(cin >> x) a[++n] = x;

    int res = 0;
    for(int i = 1; i <= n; i++){
        f[i] = 1;
        for(int j = 1; j < i; j++){
            if(a[j] < a[i]) f[i] = max(f[i], f[j] + 1);
        }
        res = max(res, f[i]);
    }

    cout << res << endl;

    int ans[N];
    int cnt = 0;
    for(int i = n; i >= 1; i--){
        if(f[i] == res){
            ans[cnt++] = a[i];
            res--;
        }
    }

    for(int i = cnt - 1; i >= 0; i--) cout << ans[i] << " ";

    cout << endl;

    return 0;
}
```



*2023-01-09 周一*