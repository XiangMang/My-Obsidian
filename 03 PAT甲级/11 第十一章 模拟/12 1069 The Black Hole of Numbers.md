## [题目详情 - 1069 The Black Hole of Numbers (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805400954585088)

[1555. 数字黑洞 - AcWing题库](https://www.acwing.com/problem/content/1557/)

#模拟 

For any 4-digit integer except the ones with all the digits being the same, if we sort the digits in non-increasing order first, and then in non-decreasing order, a new number can be obtained by taking the second number from the first one. Repeat in this manner we will soon end up at the number `6174` -- the **black hole** of 4-digit numbers. This number is named Kaprekar Constant.

For example, start from `6767`, we'll get:

```
7766 - 6677 = 1089
9810 - 0189 = 9621
9621 - 1269 = 8352
8532 - 2358 = 6174
7641 - 1467 = 6174
... ...
```

Given any 4-digit number, you are supposed to illustrate the way it gets into the black hole.

### Input Specification:

Each input file contains one test case which gives a positive integer $N$ in the range $(0,10^4)$.

### Output Specification:

If all the 4 digits of $N$ are the same, print in one line the equation `N - N = 0000`. Else print each step of calculation in a line until `6174` comes out as the difference. All the numbers must be printed as 4-digit numbers.

### Sample Input 1:

```in
6767
```

### Sample Output 1:

```out
7766 - 6677 = 1089
9810 - 0189 = 9621
9621 - 1269 = 8352
8532 - 2358 = 6174
```

### Sample Input 2:

```in
2222
```

### Sample Output 2:

```out
2222 - 2222 = 0000
```

### Idea

使用数组进行排序,反转的操作,方便处理

使用格式化输出处理前导零

对条件控制语句的分析

### AC code

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> get(int n){
    int nums[4];
    for(int i = 0; i < 4; i++){
        nums[i] = n % 10;
        n /= 10;
    }
    sort(nums, nums + 4);
    int a = 0;
    for(int i = 0; i < 4; i++) a = a * 10 + nums[i];
    reverse(nums, nums + 4);
    int b = 0;
    for(int i = 0; i < 4; i++) b = b * 10 + nums[i];

    return {b, a};
}

int main(void){

    int n;
    cin >> n;

    do{
        auto t = get(n);
        n = t[0] - t[1];
        printf("%04d - %04d = %04d\n", t[0], t[1], n);
    }while(n && n != 6174);

    return 0;
}
```


*2022-08-06 周六*