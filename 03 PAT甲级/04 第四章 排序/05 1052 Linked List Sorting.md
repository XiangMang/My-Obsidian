## [题目详情 - 1052 Linked List Sorting (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805425780670464)

[1538. 链表排序 - AcWing题库](https://www.acwing.com/problem/content/description/1540/)

#unordered_map #vector #c-str#排序

A linked list consists of a series of structures, which are not necessarily adjacent in memory. We assume that each structure contains an integer `key` and a `Next` pointer to the next structure. Now given a linked list, you are supposed to sort the structures according to their key values in increasing order.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive $N (<10^5)$ and an address of the head node, where N is the total number of nodes in memory and the address of a node is a 5-digit positive integer. NULL is represented by $−1$.

Then N lines follow, each describes a node in the format:

```
Address Key Next
```

where `Address` is the address of the node in memory, `Key` is an integer in $[−10^5,10^5]$, and `Next` is the address of the next node. It is guaranteed that all the keys are distinct and there is no cycle in the linked list starting from the head node.

### Output Specification:

For each test case, the output format is the same as that of the input, where $N$ is the total number of nodes in the list and all the nodes must be sorted order.

### Sample Input:

```in
5 00001
11111 100 -1
00001 0 22222
33333 100000 11111
12345 -1 33333
22222 1000 12345
```

### Sample Output:

```out
5 12345
12345 -1 00001
00001 0 11111
11111 100 22222
22222 1000 33333
33333 100000 -1
```

### Idea

1. 使用结构体存储链表的数据
2. 可以使用 `unordered_map` 进行数据的映射
3. 由于本题的输入数据较大,建议尽量避免使用 `cin,cout`

### AC code

#### STL

```cpp
#include <iostream>
#include <algorithm>
#include <unordered_map>
#include <vector>

using namespace std;

struct Node{
    string address;
    int key;
    string next;

    bool operator< (const Node& t) const{
        return key < t.key;
    }
};

int main(void){

    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    int n;
    string head;
    cin >> n >> head;

    unordered_map<string, Node> hash;
    string address, next;
    int key;
    while(n--){
        cin >> address >> key >> next;
        hash[address] = {address, key, next};
    }

    vector<Node> nodes;
    for(auto i = head; i != "-1"; i = hash[i].next) nodes.push_back(hash[i]);

    cout << nodes.size() << ' ';
    if(nodes.empty()) puts("-1");
    else{
        sort(nodes.begin(), nodes.end());
        cout << nodes[0].address << endl;
        for(int i = 0; i < nodes.size(); i++){
            if(i + 1 == nodes.size()) cout << nodes[i].address << ' ' << nodes[i].key << ' ' << "-1" << endl;
            else cout << nodes[i].address << ' ' << nodes[i].key << ' ' << nodes[i + 1].address << endl;
        }
    }

    return 0;
}
```

#### char数组

```cpp
#include <iostream>
#include <algorithm>
#include <unordered_map>
#include <vector>

using namespace std;

struct Node{
    string address;
    int key;
    string next;

    bool operator< (const Node& t) const{
        return key < t.key;
    }
};

int main(void){

    int n;
    char head[10];
    scanf("%d%s", &n, head);

    unordered_map<string, Node> map;
    char address[10], next[10];
    while (n -- ){
        int key;
        scanf("%s%d%s", address, &key, next);
        map[address] = {address, key, next};
    }

    vector<Node> nodes;
    for (string i = head; i != "-1"; i = map[i].next) nodes.push_back(map[i]);

    printf("%d ", nodes.size());
    if (nodes.empty()) puts("-1");
    else{
        sort(nodes.begin(), nodes.end());
        printf("%s\n", nodes[0].address.c_str());
        for (int i = 0; i < nodes.size(); i ++ ){
            if (i + 1 == nodes.size()) printf("%s %d -1\n", nodes[i].address.c_str(), nodes[i].key);
            else printf("%s %d %s\n", nodes[i].address.c_str(), nodes[i].key, nodes[i + 1].address.c_str());
        }
    }

    return 0;
}
```


*2022-07-26 周二*