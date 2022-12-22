## [题目详情 - 1004 Counting Leaves (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/994805521431773184)

[1476. 数叶子结点 - AcWing题库](https://www.acwing.com/problem/content/1478/)

#树的遍历 #DFS

A family hierarchy is usually presented by a pedigree tree. Your job is to count those family members who have no child.

### Input Specification:

Each input file contains one test case. Each case starts with a line containing $0<N<100$, the number of nodes in a tree, and $M (<N)$, the number of non-leaf nodes. Then $M$ lines follow, each in the format:

```
ID K ID[1] ID[2] ... ID[K]
```

where `ID` is a two-digit number representing a given non-leaf node, `K` is the number of its children, followed by a sequence of two-digit `ID`'s of its children. For the sake of simplicity, let us fix the root ID to be `01`.

The input ends with $N$ being $0$. That case must NOT be processed.

### Output Specification:

For each test case, you are supposed to count those family members who have no child **for every seniority level** starting from the root. The numbers must be printed in a line, separated by a space, and there must be no extra space at the end of each line.

The sample case represents a tree with only 2 nodes, where `01` is the root and `02` is its only child. Hence on the root `01` level, there is `0` leaf node; and on the next level, there is `1` leaf node. Then we should output `0 1` in a line.

### Sample Input:

```in
2 1
01 1 02
```

### Sample Output:

```out
0 1
```

### Idea

- 使用邻接表存储信息
- 由于 $BFS$ 需要自行维护一个队列, 比较麻烦. 故使用 $DFS$ 进行搜索
- 在搜索的过程中, 需要记录当前节点的编号, 以及当前节点的层数

### AC code

```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 110;

int n, m;
int h[N], e[N], ne[N], idx;// 邻接表的物理形式
int cnt[N], max_depth;// 记录每层的叶子节点的个数和最大层数

void add(int a, int b){// 添加边
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

void dfs(int u, int depth){
    if(h[u] == -1){// 如果是叶子节点
        cnt[depth]++;// 该层数量加一
        max_depth = max(max_depth, depth);
        return ;
    }

    for(int i = h[u]; ~i; i = ne[i]){
        dfs(e[i], depth + 1);// 搜索下一节点, 并将深度加一
    }
}

int main(void){

    cin >> n >> m;

    memset(h, -1, sizeof h);

    for(int i = 0; i < m; i++){
        int id, k;
        cin >> id >> k;
        while(k--){
            int son;
            cin >> son;
            add(id, son);
        }
    }

    dfs(1, 0);// 从节点1, 第0层进行搜索

    for(int i = 0; i <= max_depth; i++){
        if(!i) cout << cnt[i];
        else cout << ' ' << cnt[i];
    }

    return 0;
}
```



*2022-10-23 周日*