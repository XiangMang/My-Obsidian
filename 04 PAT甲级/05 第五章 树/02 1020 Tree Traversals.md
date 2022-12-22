## [题目详情 - 1020 Tree Traversals (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/994805485033603072)

[1497. 树的遍历 - AcWing题库](https://www.acwing.com/problem/content/1499/)

#树的构建 #树的遍历  #BFS #hash 

Suppose that all the keys in a binary tree are distinct positive integers. Given the postorder and inorder traversal sequences, you are supposed to output the level order traversal sequence of the corresponding binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer $N (≤30)$, the total number of nodes in the binary tree. The second line gives the postorder sequence and the third line gives the inorder sequence. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in one line the level order traversal sequence of the corresponding binary tree. All the numbers in a line must be separated by exactly one space, and there must be no extra space at the end of the line.

### Sample Input:

```in
7
2 3 1 5 7 6 4
1 2 3 4 5 6 7
```

### Sample Output:

```out
4 1 6 3 5 7 2
```

### Idea

样例模拟 : 

```
后序遍历 : 2 3 1 5 7 6 4
中序遍历 : 1 2 3 4 5 6 7
```

<img src="C:\Users\LONG\AppData\Local\Temp\WeChat Files\256fbe438b668d053c9249d767f6370.jpg" alt="256fbe438b668d053c9249d767f6370" style="zoom:33%;" />

- 由后序遍历知, 根节点为 4
- 则由中序遍历知, 1 2 3 构成了左子树, 5 6 7 构成了右子树
- 对于左子树, 由后序遍历知, 1 为根节点, 再由中序遍历知, 1 没有左子树, 再由后序遍历知, 3 为根节点
- 右子树, 同上

方法总结 : 

- 在后序遍历里最后一个点一定是根节点
- 在中序遍历里, 先找到根节点的位置, 再寻找其左子树与右子树

方法抽象 : 

- 先确定根节点是什么
- 再在中序遍历里找到根节点是在第几个位置出现的(可以使用hash表进行存储)
-  计算一下左子树的区间长度是多少, 从而知道左子树包含多少个点
-  由左子树的点数, 就可以知道在中序遍历里左子树的区间
- 同理处理右子树
- 递归处理以上步骤
- 再使用 $BFS$ 进行遍历

对于该题构建函数的参数的确认:

![image-20221025153534048](C:\Users\LONG\AppData\Roaming\Typora\typora-user-images\image-20221025153534048.png)

- 其左子树在中序遍历中的区间为 `[il,k-1]`
- 由图可知, 左子树在后序遍历中的区间从 `pl` 开始, 又因为在遍历中, 其区间长度应该相等, 设其右端点为 `x` , 则 `x - pl = k - 1 - rl`, 故 `x = pl + k - 1- il`
- 其右子树在中序遍历中的区间为 `[k + 1, ir]`
- 显然, 右子树在后序遍历中的区间为 `[pl + k - 1 - il + 1, pr - 1]`

如果权值不同, 则该题无法使用此方法, 因为此时二叉树可能不唯一

### AC code

```cpp
#include <iostream>
#include <cstring>
#include <queue>
#include <algorithm>
#include <unordered_map>

using namespace std;

const int N = 40;

int n;
int postorder[N], inorder[N];// 存储后序遍历与中序遍历
unordered_map<int, int> l, r, pos;
// 存储每个点的左儿子与右儿子, pos存储在中序遍历中, 每个值对应的下标是什么

int build(int il, int ir, int pl, int pr){
    // 参数为 : 中左端  中右端  后左端  后右端
    int root = postorder[pr];// 根节点为后续遍历的最后一个节点
    int k = pos[root];// 查询在中序遍历中根节点的坐标
    if(il < k){// 如果左子树存在
        l[root] = build(il, k - 1, pl, pl + k - 1 - il);// 根的左儿子就等于左子树
    }
    if(ir > k){
        r[root] = build(k + 1, ir, pl + k - 1 - il + 1, pr - 1);
    }
    return root;
}

void bfs(int root){
    int check = 0;
    queue<int> q;
    q.push(root);
    while(q.size()){
        auto t = q.front();
        q.pop();
        if(!check) check = 1, cout << t;
        else cout << ' ' << t;
        if(l.count(t)) q.push(l[t]);// 如果存在左子树, 压入队列
        if(r.count(t)) q.push(r[t]);// 右子树同理
    }
}

int main(void){

    cin >> n;
    for(int i = 0; i < n; i++) cin >> postorder[i];
    for(int i = 0; i < n; i++){
        cin >> inorder[i];
        pos[inorder[i]] = i;// 在hash表中存储在中序遍历中每个值对应的下标是什么
    }

    int root = build(0, n - 1, 0, n - 1);// 递归构建二叉树
    // 该函数参数为当前子树中序遍历和后序遍历是从第几个位置到第几个位置

    bfs(root);

    return 0;
}
```


*2022-10-23 周日*