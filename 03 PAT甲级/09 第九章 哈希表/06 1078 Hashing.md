## [题目详情 - 1078 Hashing (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805389634158592)

[1564. 哈希 - AcWing题库](https://www.acwing.com/problem/content/1566/)

#hash #开放寻址法

The task of this problem is simple: insert a sequence of distinct positive integers into a hash table, and output the positions of the input numbers. The hash function is defined to be $H(key)=key\%TSize$ where $TSize$ is the maximum size of the hash table. Quadratic probing (with positive increments only) is used to solve the collisions.

Note that the table size is better to be prime. If the maximum size given by the user is not prime, you must re-define the table size to be the smallest prime number which is larger than the size given by the user.

### Input Specification:

Each input file contains one test case. For each case, the first line contains two positive numbers: $MSize (≤10^4)$ and $N (≤MSize)$ which are the user-defined table size and the number of input numbers, respectively. Then $N$ distinct positive integers are given in the next line. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print the corresponding positions (index starts from 0) of the input numbers in one line. All the numbers in a line are separated by a space, and there must be no extra space at the end of the line. In case it is impossible to insert the number, print "`-`" instead.

### Sample Input:

```in
4 4
10 6 4 15
```

### Sample Output:

```out
0 1 4 -
```

### Idea

`Quadratic probing (with positive increments only)` : 只具有正增量的二次探测法

即插入元素发生冲突时,用发生冲突的单元 `H(key)` , 加上 $1^2,2^2\dots$，即$[H(key) + 1^2]\%S,[H(key)+2^2]\%S,\dots$直到找到空闲单元,最大增加到 ${Size}^2$

### AC code

```cpp
#include <iostream>

using namespace std;

const int N = 1e4 +10;

int s, n;// s表示hash表的长度,n表示输入的个数
int h[N];// 表示hash表

bool is_prime(int s){
    if(s < 2) return false;
    for(int i = 2; i <= s / i; i++){
        if(s % i == 0) return false;
    }
    return true;
}

int find(int x){
    int t = x % s;// 求hash值
    for(int k = 0; k < s; k++){
        int i = (t + k * k) % s;
        if(!h[i]) return i;
    }
    return -1;
}

int main(void){

    cin >> s >> n;

    while(!is_prime(s)) s++;

    for(int i = 0; i < n; i++){
        int x;
        cin >> x;
        int t = find(x);

        if(t == -1) printf("-");
        else{
            h[t] = x;
            cout << t;
        }

        if(i != n - 1) cout << ' ';
    }

    return 0;
}
```


*2022-08-06 周六*