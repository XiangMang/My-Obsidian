## [题目详情 - 1120 Friend Numbers (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805352925609984)

[1610. 朋友数 - AcWing题库](https://www.acwing.com/problem/content/1612/)

#set 

Two integers are called "friend numbers" if they share the same sum of their digits, and the sum is their "friend ID". For example, 123 and 51 are friend numbers since 1+2+3 = 5+1 = 6, and 6 is their friend ID. Given some numbers, you are supposed to count the number of different friend ID's among them.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer $N$. Then $N$ positive integers are given in the next line, separated by spaces. All the numbers are less than $10^4$.

### Output Specification:

For each case, print in the first line the number of different friend ID's among the given integers. Then in the second line, output the friend ID's in increasing order. The numbers must be separated by exactly one space and there must be no extra space at the end of the line.

### Sample Input:

```in
8
123 899 51 998 27 33 36 12
```

### Sample Output:

```out
4
3 6 9 26
```

### Idea

排序+判重

### AC code

```cpp
#include <iostream>
#include <set>

using namespace std;

int main(void){

    int n;
    cin >> n;

    set<int> s;
    while(n--){
        int tmp;
        cin >> tmp;
        int sum = 0;
        while(tmp) sum += tmp % 10, tmp /= 10;
        s.insert(sum);
    }

    cout << s.size() << endl;

    bool is_first = true;
    for(auto c : s){
        if(is_first) is_first = false;
        else cout << ' ';
        cout << c;
    }

    return 0;
}
```


*2022-08-05 周五*