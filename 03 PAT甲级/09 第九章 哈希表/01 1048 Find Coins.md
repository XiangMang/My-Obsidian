## [题目详情 - 1048 Find Coins (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805432256675840)

[1532. 找硬币 - AcWing题库](https://www.acwing.com/problem/content/1534/)

#二分 #hash #双指针 

Eva loves to collect[^1] coins from all over the universe[^2], including some other planets[^3] like Mars. One day she visited a universal shopping mall[^4] which could accept all kinds of coins as payments[^5]. However, there was a special[^6] requirement[^7] of the payment: for each bill[^8], she could only use exactly[^9] two coins to pay the exact[^10] amount[^11]. Since she has as many as $10^5$ coins with her, she definitely[^12] needs your help. You are supposed to tell her, for any given amount of money, whether or not she can find two coins to pay for it.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive numbers: $N$ ($≤10^5$, the total[^13] number of coins) and $M$ ($≤10^3$, the amount of money Eva has to pay). The second line contains $N$ face values of the coins, which are all positive numbers no more than 500. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in one line the two face values $V_1$ and $V_2$ (separated by a space) such that $V_1+V_2=M$ and $V_1≤V_2$. If such a solution is not unique[^14], output the one with the smallest $V_1$. If there is no solution, output `No Solution` instead.

### Sample Input 1:

```in
8 15
1 2 8 7 2 4 11 15
```

### Sample Output 1:

```out
4 11
```

### Sample Input 2:

```in
7 14
1 8 7 2 4 11 15
```

### Sample Output 2:

```out
No Solution
```

### Idea

- 二分
- hash(查找一个数是否存在)
- 根据单调性关系,使用双指针

### AC code

#### 二分

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e5 + 10;

int n, m;
int q[N];
int a, b;

int main(void){

    scanf("%d%d", &n, &m);

    for(int i = 0; i < n; i++) scanf("%d", &q[i]);

    sort(q, q + n);

    for(int i = 0; i < n; i++){
        int l = 0, r = n - 1;
        while(l < r){
            int mid = l + r >> 1;
            if(q[i] + q[mid] >= m) r = mid;
            else l = mid + 1;
        }
        if(q[l] + q[i] == m && i != l){// 同时确保下标不一致
            a = q[i];
            b = q[l];
            break;
        }
    }

    if(a) printf("%d %d\n", a, b);
    else puts("No Solution");

    return 0;
}
```

#### hash

```cpp
#include <iostream>
#include <algorithm>
#include <unordered_set>

using namespace std;

const int INF = 1e5;

int main(void){

    int n, m; 
    scanf("%d%d", &n, &m);
    unordered_set<int> hash;

    int v1 = INF, v2;
    for(int i = 0; i < n; i++){
        int a, b;
        scanf("%d", &a);
        b = m - a;
        if(hash.count(b)){// 判断符合要求的数是否存在
            if(a > b) swap(a, b);// 确保大小关系
            if(a < v1) v1 = a, v2 = b;// 确保是最小值
        }
        else hash.insert(a);
    }

    if(v1 == INF) puts("No Solution");
    else printf("%d %d\n", v1, v2);

    return 0;
}
```

####  双指针

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1e5 + 10;

int n, m;
int q[N];

int main(void){

    scanf("%d%d", &n, &m);
    for(int i = 0; i < n; i++) scanf("%d", &q[i]);
    sort(q, q + n);

    for(int i = 0, j = n - 1; i < j; i++){
        while(i < j && q[i] + q[j] > m) j--;
        if(i < j && q[i] + q[j] == m){
            printf("%d %d\n", q[i], q[j]);
            return 0;
        }
    }

    puts("No Solution");

    return 0;
}
```


*2022-08-04 周四*

[^1]: collect $v.$ 收集,采集
[^2]: universe $n.$ 宇宙
[^3]: planet $n.$ 行星
[^4]: mall $n.$ 购物中心
[^5]: payment $n.$ 支付额
[^6]: special $adj.$ 特别的
[^7]: requirement $n.$ 要求
[^8]: bill $n.$ 账单
[^9]: exactly $adv.$ 精确的;恰好
[^10]: exact $adj.$ 准确的
[^11]: amount $n.$ 数量,金额
[^12]: definitely $adv.$ 肯定的;明确的
[^13]: total $n.$ 总数
[^14]: unique $adj.$ 独一无二的