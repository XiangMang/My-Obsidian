##  [题目详情 - 1149 Dangerous Goods Packaging (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/1038429908921778176)

[1642. 危险品装箱 - AcWing题库](https://www.acwing.com/problem/content/1644/)

#hash 

When shipping goods with containers, we have to be careful not to pack some incompatible goods into the same container, or we might get ourselves in serious trouble. For example, oxidizing agent （氧化剂） must not be packed with flammable liquid （易燃液体）, or it can cause explosion.

Now you are given a long list of incompatible goods, and several lists of goods to be shipped. You are supposed to tell if all the goods in a list can be packed into the same container.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers: $N (≤10^4)$, the number of pairs of incompatible goods, and $M (≤100)$, the number of lists of goods to be shipped.

Then two blocks follow. The first block contains N pairs of incompatible goods, each pair occupies a line; and the second one contains M lists of goods to be shipped, each list occupies a line in the following format:

```
K G[1] G[2] ... G[K]
```

where `K` $(≤1,000)$ is the number of goods and `G[i]`'s are the IDs of the goods. To make it simple, each good is represented by a 5-digit ID number. All the numbers in a line are separated by spaces.

### Output Specification:

For each shipping list, print in a line `Yes` if there are no incompatible goods in the list, or `No` if not.

### Sample Input:

```in
6 3
20001 20002
20003 20004
20005 20006
20003 20001
20005 20004
20004 20006
4 00001 20004 00002 20003
5 98823 20002 20003 20006 10010
3 12345 67890 23333
```

### Sample Output:

```out
No
Yes
Yes
```

### Idea

本题也可以使用 `pair` 进行处理,但由于哈希表每次操作都是 $O(1)$ 的复杂度,故使用哈希表

### AC code

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

const int N = 1e4 + 10;

int n, m;
int a[N], b[N];

int main(void){

    scanf("%d%d", &n, &m);

    for(int i = 0; i < n; i++) scanf("%d%d", &a[i], &b[i]);

    while(m--){
        int k;
        scanf("%d", &k);
        unordered_set<int> s;
        while(k--){
            int x;
            scanf("%d", &x);
            s.insert(x);
        }

        bool success = true;
        for(int i = 0; i < n; i++){
            if(s.count(a[i]) && s.count(b[i])){
                success = false;
                break;
            }
        }

        if(success) puts("Yes");
        else puts("No");
    }

    return 0;
}
```


*2022-08-06 周六*