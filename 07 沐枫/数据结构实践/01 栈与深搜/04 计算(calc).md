## [题目详情 - 计算(calc) - 沐枫OJ (mfstem.org)](https://www.mfstem.org/p/632?tid=618e1a85f95440248cba192a)

#表达式求值 

### Description

小明在你的帮助下，破密了Ferrari设的密码门，正要往前走，突然又出现了一个密码门，门上有一个算式，其中只有“(”，“)”，“0-9”，“+”，“-”，“*”，“/”，“^”，求出的值就是密码。小明数学学得不好，还需你帮他的忙。(“/”用整数除法，"^"是幂运算，`2^3` 为 8)

### Format

#### Input

输入共1行，为一个算式。

#### Output

输出共1行，就是密码。

### Samples

#### 输入数据 1

```input1
1+(3+2)*(7^2+6*9)/(2)
```

#### 输出数据 1

```output1
258
```

#### 输入数据 2

```input2
3*(-21)
```

#### 输出数据 2

```output2
-63
```

### Limitation

1s, 1024KiB for each test case.

100% 的数据满足：

算式长度$≤60$，其中所有数据在 $2^{31}-1$的范围内。

#### 代码

```cpp
#include <iostream>
#include <stack>
#include <cmath>
#include <unordered_map>

using namespace std;

stack<int> num;
stack<char> op;
unordered_map<char, int> level {{'+', 1}, {'-', 1}, {'*', 2}, {'/', 2}, {'^', 3}};
// 设置运算符优先级

void eval(void){// 计算函数
    auto b = num.top(); num.pop();
    auto a = num.top(); num.pop();
    auto c = op.top(); op.pop();
    int x;
    if(c == '+') x = a + b;
    else if(c == '-') x = a - b;
    else if(c == '*') x = a * b;
    else if(c == '/') x = a / b;
    else x = pow(a, b);
    num.push(x);
}

int main(void){

    string str;
    cin >> str;

    for(int i = 0; i < str.size(); i++){
        auto c = str[i];
        if(isdigit(c)){// 如果是数字, 则把他抠出来
            int x = 0, j = i;
            while(j < str.size() && isdigit(str[j])){
                x = x  * 10 + str[j++] - '0';
            }
            i = j - 1;
            num.push(x);
        }
        else if(c == '(') op.push(c);
        else if(c == ')'){
            while(op.top() != '(') eval();
            op.pop();
        }
        else if(c == '+' || c == '-'){
            if(!isdigit(str[i - 1]) && str[i - 1] != ')'){// 判断是否是负号
                if(str[i + 1] == '('){// 如果左括号后紧跟负数
                    num.push(-1);
                    op.push('*');
                }else{
                    int j = i + 1, t = 0;// i是负号, 从i + 1开始
                    while (isdigit(str[j])){
                        t = t * 10 + str[j++] - '0';
                    }
                    num.push(-t);
                    i = j - 1;
                } 
            }
            else{
                while(op.size() && level[op.top()] >= level[c]){
                    eval();
                }
                op.push(c); 
            }
        }
        else if(c == '*' || c == '/' || c == '^'){// 对其他运算符进行运算
            while(op.size() && level[op.top()] >= level[c]){
                eval();
            }
            op.push(c); 
        }
    }

    while(op.size()) eval();// 处理剩余部分
    cout << num.top() << endl;

    return 0;
}
```




*2022-12-25 周日*