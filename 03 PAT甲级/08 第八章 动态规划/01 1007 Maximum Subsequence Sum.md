## [题目详情 - 1007 Maximum Subsequence Sum (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805514284679168)

[1479. 最大子序列和 - AcWing题库](https://www.acwing.com/problem/content/1481/)

#动态规划

Given a sequence of $K$ integers ${ N_1, N_2, ..., N_K }$. A continuous subsequence is defined to be ${ N_i, N_{i+1}, ..., N_j }$ where $1≤i≤j≤K$. The Maximum Subsequence is the continuous subsequence which has the largest sum of its elements. For example, given sequence $\{ -2, 11, -4, 13, -5, -2 \}$, its maximum subsequence is $\{ 11, -4, 13 \}$ with the largest sum being 20.

Now you are supposed to find the largest sum, together with the first and the last numbers of the maximum subsequence.

### Input Specification:

Each input file contains one test case. Each case occupies two lines. The first line contains a positive integer $K (≤10000)$. The second line contains $K$ numbers, separated by a space.

### Output Specification:

For each test case, output in one line the largest sum, together with the first and the last numbers of the maximum subsequence. The numbers must be separated by one space, but there must be no extra space at the end of a line. In case that the maximum subsequence is not unique, output the one with the smallest indices $i$ and $j$ (as shown by the sample case). If all the $K$ numbers are negative, then its maximum sum is defined to be 0, and you are supposed to output the first and the last numbers of the whole sequence.

### Sample Input:

```in
10
-10 1 2 3 4 -5 -23 3 7 -21
```

### Sample Output:

```out
10 1 4
```

### Idea

详见:[[实例1.1 最大子列和问题]]

### AC code

```cpp
#include <iostream>

using namespace std;

const int N = 1e5 + 10;

int n;
int q[N];

int main(void){

    cin >> n; 
    for(int i = 0; i < n; i++) cin >> q[i];
    
    int l = 0, r = 0;
    int ans = -1;
    for(int i = 0, f = -1, state; i < n; i++){
        if(f < 0){// 在此处不使用<=是因为题目要求输出最小的下标索引
            f = 0;
            state = i;
        }
        f += q[i];
        if(ans < f){
            ans = f;
            l = q[state];
            r = q[i];
        }
    }

    if(ans < 0) ans = 0, l = q[0], r = q[n - 1];
    cout << ans << ' ' << l << ' ' << r << endl;

    return 0;
}
```


*2022-08-06 周六*