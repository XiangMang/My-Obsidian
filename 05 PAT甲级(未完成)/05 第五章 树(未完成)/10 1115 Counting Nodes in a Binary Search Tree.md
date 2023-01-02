## [题目详情 - 1115 Counting Nodes in a Binary Search Tree (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/994805355987451904)

[1605. 二叉搜索树最后两层结点数量 - AcWing题库](https://www.acwing.com/problem/content/1607/)

#BST #DFS 

A Binary Search Tree (BST) is recursively defined as a binary tree which has the following properties:

-   The left subtree of a node contains only nodes with keys less than or equal to the node's key.
-   The right subtree of a node contains only nodes with keys greater than the node's key.
-   Both the left and right subtrees must also be binary search trees.

Insert a sequence of numbers into an initially empty binary search tree. Then you are supposed to count the total number of nodes in the lowest 2 levels of the resulting tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤1000) which is the size of the input sequence. Then given in the next line are the N integers in [−1000,1000] which are supposed to be inserted into an initially empty binary search tree.

### Output Specification:

For each case, print in one line the numbers of nodes in the lowest 2 levels of the resulting tree in the format:

```
n1 + n2 = n
```

where `n1` is the number of nodes in the lowest level, `n2` is that of the level above, and `n` is the sum.

### Sample Input:

```in
10
25 30 42 16 20 20 35 -5 28 22
```

### Sample Output:

```out
3 + 4 = 7
```

### Idea


### AC code
```cpp
#include <iostream>

using namespace std;

const int N = 1e3 + 10;

int n;
int l[N], r[N], v[N], idx;// l存储左儿子, r存储右儿子, v存储权值, idx记录编号
int cnt[N], max_depth;// cnt存储每一层的节点的个数

void insert(int& u, int w){// 根节点在插入函数中变化,故使用引用
    if(!u){
        u = ++idx;// 为根节点创建一个新节点
        v[u] = w;// 赋予权值
    }else if(w <= v[u]) insert(l[u], w);
    else insert(r[u], w);
}

void dfs(int u, int depth){
    if(!u) return ;
    cnt[depth]++;// 更新最大层数
    max_depth = max(depth, max_depth);
    dfs(l[u], depth + 1);
    dfs(r[u], depth + 1);
}

int main(void){

    cin >> n;

    int root = 0;// 根节点
    for(int i = 0; i < n; i++){
        int w;
        cin >> w;
        insert(root, w);
    }

    dfs(root, 0);// 爆搜, 寻找到每一层节点的数量

    int n1 = cnt[max_depth], n2 = cnt[max_depth - 1];
    printf("%d + %d = %d", n1, n2, n1 + n2);

    return 0;
}
```