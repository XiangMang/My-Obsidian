## [题目详情 - 1001 A+B Format (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805528788582400)

#模拟 #to_string

[1473. A + B 格式 - AcWing题库](https://www.acwing.com/problem/content/1475/)

Calculate *a*+*b* and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).

### Input Specification:

Each input file contains one test case. Each case contains a pair of integers *a* and *b* where −106≤*a*,*b*≤106. The numbers are separated by a space.

### Output Specification:

For each test case, you should output the sum of *a* and *b* in one line. The sum must be written in the standard format.

### Sample Input:

```in
-1000000 9
```

### Sample Output:

```out
-999,991
```

### Idea

处理字符串问题的工具

1. `string`
2. `char[]` （不怎么常用），但是运行效率高

思路：

1. 输入a, b
2. 计算a + b
3. 将和传化成字符串
4. 对字符串进行分隔

### AC code

```c++
#include <iostream>
#include <cstring>

using namespace std;

int main(void){

    int a, b, c;

    cin >> a >> b;
    string str = to_string(a + b);
    
    string ans;
    for(int i = str.size() - 1, j = 0; i >= 0; i--){
        ans = str[i] + ans;
        j++;
        if(j % 3 == 0 && i && str[i - 1] != '-') ans = ',' + ans;
        //每三位数加上逗号，且避免首次运算与符号
    }

    cout << ans << endl;

    return 0;
}
```


*2022-06-26 周日*