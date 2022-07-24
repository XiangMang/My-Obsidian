## [题目详情 - 1027 Colors in Mars (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805470349344768)

[1504. 火星颜色 - AcWing题库](https://www.acwing.com/problem/content/1506/)

#进位制

People in Mars represent the colors in their computers in a similar way as the Earth people. That is, a color is represented by a 6-digit number, where the first 2 digits are for `Red`, the middle 2 digits for `Green`, and the last 2 digits for `Blue`. The only difference is that they use radix 13 (0-9 and A-C) instead of 16. Now given a color in three decimal numbers (each between 0 and 168), you are supposed to output their Mars RGB values.

### Input Specification:

Each input file contains one test case which occupies a line containing the three decimal color values.

### Output Specification:

For each test case you should output the Mars RGB value in the following format: first output `#`, then followed by a 6-digit number where all the English characters must be upper-cased. If a single color is only 1-digit long, you must print a `0` to its left.

### Sample Input:

```in
15 43 71
```

### Sample Output:

```out
#123456
```

### Idea

数字不足两位,需要不足两位,使用 `int` 型不利于操作,可以使用 `char` 类型进行操作

### AC code

```cpp
#include <iostream>

using namespace std;

int q[3];

char get(int n){
    if(n <= 9) return n + '0';
    return n + 'A' - 10;
}

int main(void){

    for(int i = 0; i < 3; i++) cin >> q[i];

    cout << '#';
    for(int i = 0; i < 3; i++) cout << get(q[i] / 13) << get(q[i] % 13);
    cout << endl;

    return 0;
}
```


*2022-07-24 周日*