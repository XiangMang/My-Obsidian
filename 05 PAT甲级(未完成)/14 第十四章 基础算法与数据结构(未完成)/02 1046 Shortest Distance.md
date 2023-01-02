## [题目详情 - 1046 Shortest Distance (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805435700199424)

[1530. 最短距离 - AcWing题库](https://www.acwing.com/problem/content/description/1532/)

#前缀和 

The task is really simple: given $N$ exits on a highway which forms a simple cycle, you are supposed to tell the shortest distance between any pair of exits.

### Input Specification:

Each input file contains one test case. For each case, the first line contains an integer $N (in [3,10^5])$, followed by $N$ integer distances $D_1 D_2 ⋯ D_N$, where $D_i$ is the distance between the $i$-th and the $(i+1)$-st exits, and DN is between the $N$-th and the 1st exits. All the numbers in a line are separated by a space. The second line gives a positive integer $M (≤10^4)$, with $M$ lines follow, each contains a pair of exit numbers, provided that the exits are numbered from $1$ to $N$. It is guaranteed that the total round trip distance is no more than $10^7$.

### Output Specification:

For each test case, print your results in $M$ lines, each contains the shortest distance between the corresponding given pair of exits.

### Sample Input:

```in
5 1 2 4 14 9
3
1 3
2 5
4 1
```

### Sample Output:

```out
3
10
7
```

### Idea

- 考虑到路程的长弧与短弧,使用前缀和
- $s[i]$ 代表从 $1$ 走到 $i-1$ 的路程

### AC code

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e5 + 10;

int n, m;
int q[N];
int s[N];

int main(void){

    scanf("%d", &n);
    for(int i = 1; i <= n; i++) scanf("%d", &q[i]);

    for(int i = 1; i <= n; i++) s[i] = s[i - 1] + q[i];

    scanf("%d", &m);
    while(m--){
        int a, b;
        scanf("%d%d", &a, &b);
        int sum1 = 0, sum2 = 0;
        if(a > b) swap(a, b);

        sum1 = s[b - 1] - s[a - 1];
        sum2 = s[n] - s[b - 1] + s[a - 1];
        printf("%d\n", min(sum1, sum2));
    }

    return 0;
}
```


*2022-07-28 周四*