## [题目详情 - 1024 Palindromic Number (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805476473028608)

[1501. 回文数 - AcWing题库](https://www.acwing.com/problem/content/1503/)

#回文数 #高精度 #vector 

A number that will be the same when it is written forwards[^1] or backwards[^2] is known as a **Palindromic[^3] Number**. For example, $1234321$ is a palindromic number. All single digit numbers are palindromic numbers.

Non-palindromic numbers can be paired with[^4] palindromic ones via[^5] a series[^6] of operations. First, the non-palindromic number is reversed and the result is added to the original number. If the result is not a palindromic number, this is repeated[^7] until it gives a palindromic number. For example, if we start from $67$, we can obtain a palindromic number in $2$ steps: $67 + 76 = 143$, and $143 + 341 = 484$.

Given any positive integer $N$, you are supposed to find its paired palindromic number and the number of steps taken to find it.

### Input Specification:

Each input file contains one test case. Each case consists of two positive numbers $N$ and $K$, where $N (≤10^{10})$ is the initial[^8] numer and $K~(≤100)$ is the maximum number of steps. The numbers are separated by a space.

### Output Specification:

For each test case, output two numbers, one in each line. The first number is the paired palindromic number of $N$, and the second number is the number of steps taken to find the palindromic number. If the palindromic number is not found after $K$ steps, just output the number obtained at the $K$th step and $K$ instead[^9].

### Sample Input 1:

```in
67 3
```

### Sample Output 1:

```out
484
2
```

### Sample Input 2:

```in
69 3
```

### Sample Output 2:

```out
1353
3
```

### Idea

1. 使用vector存储数字,配合使用高精度加法
2. 使用 `vector<int> b(a.rbegin(), a.rend());` 将数字反转

### AC code

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> add(vector<int>& a, vector<int>& b){
    vector<int> c;
    int t = 0;
    for(int i = 0; i < a.size(); i++){
        t += a[i] + b[i];
        c.push_back(t % 10);
        t /= 10;
    }
    if(t) c.push_back(1);
    return c;
}

bool check(vector<int>& num){// 判断回文数
    for(int i = 0, j = num.size() - 1; i < j; i++, j--){
        if(num[i] != num[j]) return false;
    }
    return true;
}

int main(void){

    string n;
    int k;
    cin >> n >> k;

    vector<int> a;
    for(int i = n.size() - 1; i >= 0; i--) a.push_back(n[i] - '0');

    int cnt = 0;
    if(!check(a)){
        while(cnt < k){
            vector<int> b(a.rbegin(), a.rend());
            a = add(a, b);
            cnt++;
            if(check(a)) break;
        }
    }

    for(int i = a.size() - 1; i >= 0; i--) cout << a[i];
    cout << endl << cnt << endl;

    return 0;
}
```


相关题目
1. [[11 1040 Longest Symmetric String]]
2. [[06 1136 A Delayed Palindrome]]


*2022-07-20 周三*

[^1]: forward $adj.$ 向前的
[^2]: backward $adj.$ 向后的
[^3]: palindromic $adj.$ 回文的
[^4]: pair with 与......配对
[^5]: via $prep$ 通过
[^6]: series $n.$ 连续
[^7]: repeat $v.$ 重复
[^8]: initial $adj.$ 最初的
[^9]: instead $adv.$ 顶替, 代替