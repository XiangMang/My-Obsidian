## [题目详情 - 1005 Spell It Right (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805519074574336)

[1477. 拼写正确 - AcWing题库](https://www.acwing.com/problem/content/1479/)

#模拟 #to_string #字符串 #简单

Given a non-negative integer *N*, your task is to compute the sum of all the digits of *N*, and output every digit of the sum in English.

### Input Specification:

Each input file contains one test case. Each case occupies one line which contains an *N* (≤$10^{100}$).

### Output Specification:

For each test case, output in one line the digits of the sum in English words. There must be one space between two consecutive words, but no extra space at the end of a line.

### Sample Input:

```in
12345
```

### Sample Output:

```out
one five
```

### Idea

先使用 $string$ 将 $N$ 读入，然后转换成 $int$ 进行相加处理，最后再通过 $string$ 进行输出

### AC code

```cpp
#include <iostream>
#include <cstring>

using namespace std;

int main(void){

    string num;
    cin >> num;

    int sum = 0;
    for(auto c : num) sum += c - '0';

    string str = to_string(sum);
    string name[] = {
        "zero", "one", "two", "three", "four",
        "five", "six", "seven", "eight", "nine"
    };

    cout << name[str[0] - '0'];//PAT会卡space，所以先输出第一个，剩余的向前补空格
    for(int i = 1; i < str.size(); i++) cout << ' ' << name[str[i] - '0'];

    return 0;
}
```


*2022-06-29 周三*