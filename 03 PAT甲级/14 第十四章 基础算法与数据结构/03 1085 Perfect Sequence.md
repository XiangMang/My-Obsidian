## [题目详情 - 1085 Perfect Sequence (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805381845336064)

[1571. 完美序列 - AcWing题库](https://www.acwing.com/problem/content/1573/)

#双指针 #二分

Given a sequence of positive integers and another positive integer $p$. The sequence is said to be a perfect sequence if $M≤m×p$ where $M$ and m are the maximum and minimum numbers in the sequence, respectively.

Now given a sequence and a parameter $p$, you are supposed to find from the sequence as many numbers as possible to form a perfect subsequence.

### Input Specification:

Each input file contains one test case. For each case, the first line contains two positive integers $N$ and $p$, where $N (≤10^5)$ is the number of integers in the sequence, and $p (≤10^9)$ is the parameter. In the second line there are $N$ positive integers, each is no greater than $10^9$.

### Output Specification:

For each test case, print in one line the maximum number of integers that can be chosen to form a perfect subsequence.

### Sample Input:

```in
10 8
2 3 20 4 5 1 6 7 8 9
```

### Sample Output:

```out
8
```

### Idea

- 使用 `sort` 先进行预处理,然后使用二分出答案
- 当 $M$ 向右移动时, $m$  一定不会向左移动,故可以使用双指针

### AC code

#### 二分

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e5 +10;

int n, p;
int q[N];

int main(void){

    scanf("%d%d", &n, &p);
    for(int i = 0; i < n; i++) scanf("%d", &q[i]);

    sort(q, q + n);

    int res = 0;
    for(int i = 0; i < n; i++){
        int l = 0, r = i;
        while(l < r){
            int mid = l + r >> 1;
            if((long long)q[mid] * p >= q[i]) r = mid;
            else l = mid + 1;
        }
        res = max(res, i - l + 1);
    }

    printf("%d\n", res);

    return 0;
}
```

#### 双指针

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e5 + 10;

int n, p;
int q[N];

int main(void){

    scanf("%d%d", &n, &p);
    for(int i = 0; i < n; i++) scanf("%d", &q[i]);

    sort(q, q + n);

    int res = 0;
    for(int i = 0, j = 0; i < n; i++){
        while((long long)q[j] * p < q[i]) j++;
        res = max(res, i - j + 1);
    }

    printf("%d\n", res);

    return 0;
}
```


*2022-07-28 周四*