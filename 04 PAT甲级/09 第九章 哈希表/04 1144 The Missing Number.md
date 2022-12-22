## [题目详情 - 1144 The Missing Number (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805343463260160)

[1637. 漏掉的数字 - AcWing题库](https://www.acwing.com/problem/content/1639/)

#hash 

Given N integers, you are supposed to find the smallest positive integer that is NOT in the given list.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer $N (≤10^5)$. Then N integers are given in the next line, separated by spaces. All the numbers are in the range of **int**.

### Output Specification:

Print in a line the smallest positive integer that is missing from the input list.

### Sample Input:

```in
10
5 -25 9 6 1 3 4 2 5 17
```

### Sample Output:

```out
7
```

### AC code

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

int main(void){

    int n;
    cin >> n;

    unordered_set<int> s;
    while(n--){
        int tmp;
        cin >> tmp;
        s.insert(tmp);
    }

    int res = 1;
    while(s.count(res)) res++;

    cout << res << endl;

    return 0;
}
```


*2022-08-05 周五*