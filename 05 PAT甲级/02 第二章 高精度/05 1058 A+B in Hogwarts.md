## [题目详情 - 1058 A+B in Hogwarts (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805416519647232)

[1544. 霍格沃茨的 A + B - AcWing题库](https://www.acwing.com/problem/content/1546/)

#简单 

If you are a fan of Harry Potter, you would know the world of magic has its own currency system -- as Hagrid explained it to Harry, "Seventeen silver Sickles to a Galleon and twenty-nine Knuts to a Sickle, it's easy enough." Your job is to write a program to compute $A+B$ where $A$ and $B$ are given in the standard form of `Galleon.Sickle.Knut` (`Galleon` is an integer in $[0,10^7]$, `Sickle` is an integer in $[0, 17)$, and `Knut` is an integer in $[0, 29)$).

### Input Specification:

Each input file contains one test case which occupies a line with $A$ and $B$ in the standard form, separated by one space.

### Output Specification:

For each test case you should output the sum of $A$ and $B$ in one line, with the same format as the input.

### Sample Input:

```in
3.2.1 10.16.27
```

### Sample Output:

```out
14.1.28
```

### AC code

```cpp
#include <iostream>

using namespace std;

int a, b, c;
int tmp1, tmp2, tmp3;

int main(void){

    scanf("%d.%d.%d %d.%d.%d", &a, &b, &c, &tmp1, &tmp2, &tmp3);

    a += tmp1, b += tmp2, c += tmp3;

    while(c >= 29) c -= 29, b++;
    while(b >= 17) b -= 17, a++;

    printf("%d.%d.%d", a, b, c);

    return 0;
}
```


*2022-07-20 周三*