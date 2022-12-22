## [题目详情 - 6-1 Evaluate Postfix Expression (pintia.cn)](https://pintia.cn/problem-sets/1569112583808684032/exam/problems/1569112667996749855)

Write a program to evaluate a postfix expression. You only have to handle four kinds of operators: +, -, x, and /.

### Format of functions:

```cpp
ElementType EvalPostfix( char *expr );
```

where `expr` points to a string that stores the postfix expression. It is guaranteed that there is exactly one space between any two operators or operands.
The function `EvalPostfix` is supposed to return the value of the expression. If it is not a legal postfix expression, `EvalPostfix` must return a special value `Infinity` which is defined by the judge program.

### Sample program of judge:

```cpp
#include <stdio.h>
#include <stdlib.h>

typedef double ElementType;
#define Infinity 1e8
#define Max_Expr 30   /* max size of expression */

ElementType EvalPostfix( char *expr );

int main()
{
    ElementType v;
    char expr[Max_Expr];
    gets(expr);
    v = EvalPostfix( expr );
    if ( v < Infinity )
        printf("%f\n", v);
    else
        printf("ERROR\n");
    return 0;
}

/* Your function will be put here */
```

### Sample Input 1:

```in
11 -2 5.5 * + 23 7 / -
```

### Sample Output 1:

```out
-3.285714
```

### Sample Input 2:

```
11 -2 5.5 * + 23 0 / -
```

### Sample Output 2:

```
ERROR
```

### Sample Input 3:

```
11 -2 5.5 * + 23 7 / - *
```

### Sample Output 3:

```
ERROR
```

### Idea

后缀表达式的计算需要用栈, 具体步骤如下:

- 1. 遇到数字则入栈
  2. 遇到运算符号则从栈中取出两个数进行运算
  3. 若表达式正确,计算结束后栈中应只有一个数字作为结果

  - 在计算过程中需要注意以下几种错误
    1. 遇到运算符时,栈中数字不足两个
    2. 遇到出发运算符时栈顶元素为`0`
    3. 运算结束后栈中数字数量不为`1`

  - 需要注意几种错误情况
    1. 除数为`0`
    2. 运算时元素不足
    3. 运算结束后数字多余

### AC code

```cpp
/* Your function will be put here */
ElementType EvalPostfix(char *expr){
    double ans;// 作为最终的答案
    double numStack[Max_Expr];// 用来存储数值
    int numStackTop = 0, numStackBase = 0;
    char tmp[Max_Expr];
    int exprHead = 0, exprTail = 0;// 用来维护运算数
    for(int i = 0; expr[i] != '\0'; i++, exprTail++){
        if((expr[i] == '+' || expr[i] == '-' || expr[i] == '*' || expr[i] == '/') && (expr[i + 1] < '0' || expr[i + 1] > '9')){
            // 判断当前位置为运算符
            if(numStackTop - numStackBase < 2) return Infinity;// 如果计算时栈内元素少于两个,则表达式错误
            if(expr[i] == '+'){
                ans = numStack[numStackTop - 2] + numStack[numStackTop - 1];// 取栈顶的两个元素进行运算
                numStackTop -= 2;// 将栈顶两个元素弹出
                numStack[numStackTop++] = ans;// 将计算之后的答案压入栈中
            }else if(expr[i] == '-'){
                ans = numStack[numStackTop - 2] - numStack[numStackTop - 1];
                numStackTop -= 2;
                numStack[numStackTop++] = ans;
            }else if(expr[i] == '*'){
                ans = numStack[numStackTop - 2] * numStack[numStackTop - 1];
                numStackTop -= 2;
                numStack[numStackTop++] = ans;
            }else if(expr[i] == '/'){
                if(numStack[numStackTop - 1] == 0) return Infinity;// 如果除数为0,则表达式错误
                ans = numStack[numStackTop - 2] / numStack[numStackTop - 1];
                numStackTop -= 2;
                numStack[numStackTop++] = ans;
            }
            if(expr[i + 1] == '\0') break;// 如果是结尾,则跳出
            i++;// 永远让exprHead不在space上,确保tmp中的数值是正确的
            exprTail = i;
            exprHead = i + 1;
        }else if(expr[i] == ' '){// 如果space前面是数字,则添加到栈顶
            int j = 0;
            for(j = 0; exprHead < exprTail; j++, exprHead++){
                tmp[j] = expr[exprHead];
            }
            tmp[j] = '\0';
            exprHead = exprTail + 1;
            numStack[numStackTop++] = atof(tmp);
        }else if(expr[i + 1] == '\0'){// 处理只有一个数值输入的情况
            int j = 0;
            for(j = 0; exprHead <= exprTail; j++, exprHead++){
                tmp[j] = expr[exprHead];
            }
            tmp[j] = '\0';
            exprHead = exprTail + 1;
            numStack[numStackTop++] = atof(tmp);
        }
    }
    if(numStackTop != 1) return Infinity;
    else return numStack[numStackTop - 1];
}
```

