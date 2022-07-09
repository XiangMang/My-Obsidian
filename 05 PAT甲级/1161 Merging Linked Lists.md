## [题目详情 - 1161 Merging Linked Lists (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/1478635524918910976)

[4273. 链表合并 - AcWing题库](https://www.acwing.com/problem/content/4276/)

#静态链表 #合并 #静态链表

Given two singly linked lists $L_1=a_1→a_2→⋯→a_{n−1}→a_n$ and $L_2=b_1→b_2→⋯→b_{m−1}→b_m$. If $n≥2m$, you are supposed to reverse and merge the shorter one into the longer one to obtain a list like $a_1→a_2→b_m→a_3→a_4→b_{m−1}⋯$. For example, given one list being $6→7$ and the other one $1→2→3→4→5$, you must output $1→2→7→3→4→6→5$.

### Input Specification:

Each input file contains one test case. For each case, the first line contains the two addresses of the first nodes of $L_1$ and $L_2$, plus a positive $N (≤10^5)$ which is the total number of nodes given. The address of a node is a 5-digit nonnegative integer, and NULL is represented by `-1`.

Then N lines follow, each describes a node in the format:

```
Address Data Next
```

where `Address` is the position of the node, `Data` is a positive integer no more than 105, and `Next` is the position of the next node. It is guaranteed that no list is empty, and the longer list is at least twice as long as the shorter one.

### Output Specification:

For each case, output in order the resulting linked list. Each node occupies a line, and is printed in the same format as in the input.

### Sample Input:

```in
00100 01000 7
02233 2 34891
00100 6 00001
34891 3 10086
01000 1 02233
00033 5 -1
10086 4 00033
00001 7 -1
```

### Sample Output:

```out
01000 1 02233
02233 2 00001
00001 7 34891
34891 3 10086
10086 4 00100
00100 6 00033
00033 5 -1
```

### Idea

1. 读取所有链表
2. 对第二个链表进行反转
3. 对两个链表进行归并

### AC Code

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int N = 1e5 +10;

int h1, h2, n;
int v[N], ne[N];

int main(void){

    scanf("%d%d%d", &h1, &h2, &n);
    while(n--){// 先将所有数据存储到数组中
        int addr, val, next;
        scanf("%d%d%d", &addr, &val, &next);
        v[addr] = val, ne[addr] = next;
    }

    vector<pair<int, int>> a, b;// 将链表存储到vector
    for(int i = h1; i != -1; i = ne[i]) a.push_back({i, v[i]});
    for(int i = h2; i != -1; i = ne[i]) b.push_back({i, v[i]});
 
    if(a.size() < b.size()) swap(a, b);// 确保长度长的vector为a

    vector<pair<int, int>> c;// 合并vector
    for(int i = 0, j = b.size() - 1; i < a.size(); i += 2, j--){
        c.push_back(a[i]);
        if(i + 1 < a.size()) c.push_back(a[i + 1]);
        if(j >= 0) c.push_back(b[j]);
    }

    for(int i = 0; i < c.size(); i++){
        printf("%05d %d ", c[i].first, c[i].second);
        if(i + 1 < c.size()) printf("%05d\n", c[i + 1].first);
        else puts("-1");
    }

    return 0;
}
```

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <vector>

using namespace std;

const int N = 100010;

int f1, f2, n;
int e[N], ne[N];

vector<int> a, b, res;

int main(void){
    
    cin >> f1 >> f2 >> n;
    for (int i = 0; i < n; i ++ ){
        int address;
        cin >> address;
        cin >> e[address] >> ne[address];// 分别为当前结点数值， 和下一个结点的地址
    }

    for(int i = f1; ~i; i = ne[i]) a.push_back(i);//链表a
    for(int i = f2; ~i; i = ne[i]) b.push_back(i);//链表b
    if(a.size() < b.size()) swap(a, b);//始终让b是最短的
    reverse(b.begin(), b.end());//反转最短的链表

    for (int i = 0, j = 0; i < a.size(); ){
        res.push_back(a[i ++ ]);//插入一个链表a的结点
        if (i % 2 == 0 && j < b.size()) res.push_back(b[j ++ ]);//插入一个链表b的结点
    }

    for (int i = 0; i < res.size(); i ++ ){
        printf("%05d %d ", res[i], e[res[i]]);//输出答案链表结点的地址和当前结点的数值
        if (i == res.size() - 1) printf("-1\n");//假如是最后一个结点，输出-1
        else printf("%05d\n", res[i + 1]);//否则输出下一个结点的地址
    }

    return 0;//圆满结束
}
```


*2022-07-09 周六*