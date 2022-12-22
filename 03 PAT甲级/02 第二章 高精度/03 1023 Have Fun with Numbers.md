## [题目详情 - 1023 Have Fun with Numbers (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805478658260992)

[1500. 趣味数字 - AcWing题库](https://www.acwing.com/problem/content/1502/)

#高精度 #vector 

Notice that the number 123456789 is a 9-digit number consisting exactly[^1] the numbers from 1 to 9, with no duplication[^2]. Double it we will obtain[^3] 246913578, which happens to be another 9-digit number consisting exactly the numbers from 1 to 9, only in a different permutation[^4]. Check to see the result if we double it again!

Now you are suppose to check if there are more numbers with this property[^5]. That is, double a given number with *k* digits, you are to tell[^6] if the resulting number consists of only a permutation of the digits in the original number.

### Input Specification:

Each input contains one test case. Each case contains one positive integer with no more than 20 digits.

### Output Specification:

For each test case, first print in a line "Yes" if doubling the input number gives a number that consists of only a permutation of the digits in the original number, or "No" if not. Then in the next line, print the doubled number.

### Sample Input:

```in
1234567899
```

### Sample Output:

```out
Yes
2469135798
```

### Idea

1. 高精度乘法
2. 判断两个数组的组成是否一致
   - 使用数组进行判断
   - 使用排序进行判断

### AC code

###### 数组判断

```cpp
#include <iostream>
#include <vector>

using namespace std;

int no[11];
vector<int> num1, num2;

void mul(vector<int> &num1){
    int t = 0;
    for(int i = 0; i < num1.size() || t; i++){
        if(i < num1.size()) t += num1[i] * 2;
        num2.push_back(t % 10);
        t /= 10;
    }
    while(num2.size() > 1 && num2.back() == 0) num2.pop_back();
}

int main(void){

    string str;
    cin >> str;

    for(int i = str.size() - 1; i >= 0; i--){
        num1.push_back(str[i] - '0');
        no[str[i] - '0']++;
    }

    mul(num1);

    for(auto c : num2){
        no[c]--;
    }

    bool exit = false;
    for(auto c : no){
        if(c < 0){
            exit = true;
            break;
        }
    }
    if(!exit) printf("Yes\n");
    else printf("No\n");

    for(int i = num2.size() - 1; i >= 0; i--){
        printf("%d", num2[i]);
    }

    return 0;
}
```

###### 排序判断

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> num1, num2, num3;

void mul(vector<int> &num1){
    int t = 0;
    for(int i = 0; i < num1.size() || t; i++){
        if(i < num1.size()) t += num1[i] * 2;
        num2.push_back(t % 10);
        t /= 10;
    }
    while(num2.size() > 1 && num2.back() == 0) num2.pop_back();
}

int main(void){

    string str;
    cin >> str;

    for(int i = str.size() - 1; i >= 0; i--){
        num1.push_back(str[i] - '0');
    }

    mul(num1);

    num3 = num2;
    sort(num1.begin(), num1.end());
    sort(num2.begin(), num2.end());

    if(num1 == num2) puts("Yes");
    else puts("No");

    for(int i = num3.size() - 1; i >= 0; i--){
        printf("%d", num3[i]);
    }

    return 0;
}
```


*2022-07-19 周二*

[^1]: exactly $adv.$ 恰好
[^2]: deplication $n.$ 重复
[^3]: obtain $v.$ 获得
[^4]: permutation $n.$ 排列
[^5]: property $n.$ 性质
[^6]: tell $v.$ 辨别