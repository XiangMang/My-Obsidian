## [题目详情 - 1001 A+B Format (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805528788582400)

[1473. A + B 格式 - AcWing题库](https://www.acwing.com/problem/content/1475/)

#模拟 #to_string #字符串 #简单 

Calculate[^1] *a*+*b* and output the sum in standard[^2] format[^3] -- that is, the digits[^4] must be separated[^5] into groups[^6] of three by commas[^7] (unless there are less than four digits).

### Input Specification[^8]:

Each input file contains one test case. Each case contains a pair of integers[^9] $a$ and $b$ where $−10^6≤a,b≤10^6$. The numbers are separated by a space.

### Output Specification:

For each test case, you should output the sum of $a$ and $b$ in one line. The sum must be written in the standard format.

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

- 具体细节:
1. 每经过三个数就加上 `,`
2. `,` 不要加在第一位
3. `,` 不要加在负号后面

### AC code

```cpp
#include <iostream>
#include <cstring>

using namespace std;

int main(void){

    int a, b;

    cin >> a >> b;
    string str = to_string(a + b);
    
    string ans;
    for(int i = str.size() - 1, j = 0; i >= 0; i--){
        ans = str[i] + ans;
        j++;
        if(j % 3 == 0 && i && str[i - 1] != '-') ans = ',' + ans;
        // 使用i进行字符串的遍历,使用j来判断是否需要加逗号
        //每三位数加上逗号，且避免首次运算与符号
    }

    cout << ans << endl;

    return 0;
}
```


*2022-06-26 周日*

[^1]: calculate $v.$ 计算,核算;预测,推测
[^2]: standard $adj.$ 普通的，标准的;权威的，广泛认可的;
[^3]: format $n.$ 格式;
[^4]: digit $n.$ (零到九中的任一)数字;
[^5]: separated $v.$ (使)分开,分离
[^6]: group $n.$ 组,群
[^7]: comma $n.$ 逗号
[^8]: specification $n.$ 规格,规范
[^9]: integer $n.$ 整数