## [题目详情 - 1145 Hashing - Average Search Time (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805343236767744)

[1638. 哈希 - 平均查找时间 - AcWing题库](https://www.acwing.com/problem/content/1640/)

#hash #开放寻址法

The task of this problem is simple: insert a sequence of distinct positive integers into a hash table first. Then try to find another sequence of integer keys from the table and output the average search time (the number of comparisons made to find whether or not the key is in the table). The hash function is defined to be $H(key)=key\%TSize$ where $TSize$ is the maximum size of the hash table. Quadratic probing (with positive increments only) is used to solve the collisions.

Note that the table size is better to be prime. If the maximum size given by the user is not prime, you must re-define the table size to be the smallest prime number which is larger than the size given by the user.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 3 positive numbers: $MSize$, $N$, and $N$, which are the user-defined table size, the number of input numbers, and the number of keys to be found, respectively. All the three numbers are no more than $10^4$. Then $N$ distinct positive integers are given in the next line, followed by $N$ positive integer keys in the next line. All the numbers in a line are separated by a space and are no more than $10^5$.

### Output Specification:

For each test case, in case it is impossible to insert some number, print in a line `X cannot be inserted.` where `X` is the input number. Finally print in a line the average search time for all the M keys, accurate up to 1 decimal place.

### Sample Input:

```in
4 5 4
10 6 4 15 11
11 4 15 2
```

### Sample Output:

```out
15 cannot be inserted.
2.8
```

### Idea
详见:[[06 1078 Hashing]]

### AC code

```cpp
#include <iostream>

using namespace std;

const int N = 1e4 + 10;

int s, n, m;
int h[N];

bool is_prime(int x){
    if(x < 2) return false;
    for(int i = 2; i <= x / i; i++){
        if(x % i == 0) return false;
    }
    return true;
}

int find(int x, int& cnt){
    int t = x % s;
    cnt = 1;
    for(int k = 0; k < s; k++, cnt++){
        int i = (t + k * k) % s;
        if(!h[i] || h[i] == x) return i;
    }
    return -1;
}

int main(void){

    cin >> s >> n >> m;

    while(!is_prime(s)) s++;

    for(int i = 0; i < n; i++){
        int x, count;
        cin >> x;

        int t = find(x, count);
        if(t == -1) printf("%d cannot be inserted.\n", x);
        else h[t] = x;
    }

    int cnt = 0;
    for(int i = 0; i < m; i++){
        int x, count;
        cin >> x;
        find(x, count);
        cnt += count;
    }

    printf("%.1lf\n", (double)cnt / m);

    return 0;
}
```


*2022-08-06 周六*