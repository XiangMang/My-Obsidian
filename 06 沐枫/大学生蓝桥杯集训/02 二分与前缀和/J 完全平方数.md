### [题目详情 - 完全平方数 - 沐枫OJ (mfstem.org)](https://www.mfstem.org/p/1785?tid=63ab8e45485e4d04afcbbc34)

#打表

输入一个整数 $n(1\le n\le 10^9)$，请判断 $1!+2!+\dots +n!$ 是否为完全平方数，如果是，请输出它的正整数平方根，否则输出 `NO`

#### 输入格式

多组测试样例，每组输入一个整数 $n$。

#### 输出格式

对于每个输入 $n$，输出其对应的正整数平方根或 `NO`，每次输出占一行。

#### 输入样例

```
1
2
3
```

#### 输出样例

```
1
NO
3
```

#### 思路

设 $a_n=n!$, $S_n=1!+2!+ \dots +n!$

由**人类的智慧**知, 只有当 $n=1,3$ 时, $S_n$才是完全平方数

#### 代码

```cpp
#include <iostream>

using namespace std;

int main(){

    int n;
    while(cin >> n){
        if(n == 1) puts("1");
        else if(n == 3) puts("3");
        else puts("NO");
    }

    return 0;
}
```




*2022-12-30 周五*