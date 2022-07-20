## [题目详情 - 1040 Longest Symmetric String (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805446102073344)

[1524. 最长回文子串 - AcWing题库](https://www.acwing.com/problem/content/description/1526/)

#回文数 #双指针

Given a string, you are supposed to output the length of the longest symmetric sub-string. For example, given `Is PAT&TAP symmetric?`, the longest symmetric sub-string is `s PAT&TAP s`, hence you must output `11`.

### Input Specification:

Each input file contains one test case which gives a non-empty string of length no more than 1000.

### Output Specification:

For each test case, simply print the maximum length in a line.

### Sample Input:

```in
Is PAT&TAP symmetric?
```

### Sample Output:

```out
11
```

#### Idea

使用两个for循环进行嵌套遍历,在第二层for循环中使用双指针进行判断

回文数分为两种情况

1. 回文数的位数为奇数 `int l = i - 1, r = i + 1;`
2. 回文数的位数为偶数 `int l = i, r = i + 1;`

### AC code

```cpp
#include <iostream>

using namespace std;

int main(void){

    string str;
    getline(cin, str);

    int res = 0;
    for(int i = 0; i < str.size(); i++){
        int l = i - 1, r = i + 1;// 奇数情况
        while(l >= 0 && r < str.size() && str[l] == str[r]) l--, r++;
        res = max(res, r - l - 1);

        l = i, r = i + 1;// 偶数情况
        while(l >= 0 && r < str.size() && str[l] == str[r]) l--, r++;
        res = max(res, r - l - 1);
    }

    cout << res << endl;

    return 0;
}
```




*2022-07-20 周三*