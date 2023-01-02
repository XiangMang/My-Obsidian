## [题目详情 - 1063 Set Similarity (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805409175420928)

[1549. 集合相似度 - AcWing题库](https://www.acwing.com/problem/content/1551/)

#hash #容斥原理

Given two sets of integers, the similarity of the sets is defined to be $N_c/N_t×100\%$, where $N_c$ is the number of distinct common numbers shared by the two sets, and $N_t$ is the total number of distinct numbers in the two sets. Your job is to calculate the similarity of any given pair of sets.

### Input Specification:

Each input file contains one test case. Each case first gives a positive integer $N (≤50)$ which is the total number of sets. Then $N$ lines follow, each gives a set with a positive $M (≤10^4)$ and followed by $M$ integers in the range $[0,10^9]$. After the input of sets, a positive integer $K (≤2000)$ is given, followed by $K$ lines of queries. Each query gives a pair of set numbers (the sets are numbered from 1 to N). All the numbers in a line are separated by a space.

### Output Specification:

For each query, print in one line the similarity of the sets, in the percentage form accurate up to 1 decimal place.

### Sample Input:

```in
3
3 99 87 101
4 87 101 5 87
7 99 101 18 5 135 18 99
2
1 2
1 3
```

### Sample Output:

```out
50.0%
33.3%
```

### Idea

在计算 $N_t$ 时,使用容斥原理

### AC code

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

const int N = 55;

int n;
unordered_set<int> s[N];

int main(void){

    scanf("%d", &n);

    for(int i = 1; i <= n; i++){
        int m;
        scanf("%d", &m);
        while(m--){
            int x;
            scanf("%d", &x);
            s[i].insert(x);
        }
    }

    int m;
    scanf("%d", &m);
    while(m--){
        int a, b;
        scanf("%d%d", &a, &b);
        int nc = 0;
        for(auto c : s[a]) nc += s[b].count(c);
        int nt = s[a].size() + s[b].size() - nc;
        printf("%.1lf%%\n", (double)nc / nt * 100);
    }

    return 0;
}
```


*2022-08-05 周五*