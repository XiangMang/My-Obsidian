## [题目详情 - 1050 String Subtraction (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805429018673152)

[1534. 字符串减法 - AcWing题库](https://www.acwing.com/problem/content/1536/)

#hash #字符串 #unordered_set

Given two strings *S*1 and *S*2, *S*=*S*1−*S*2 is defined to be the remaining string after taking all the characters in *S*2 from *S*1. Your task is simply to calculate *S*1−*S*2 for any given strings. However, it might not be that simple to do it **fast**.

### Input Specification:

Each input file contains one test case. Each case consists of two lines which gives *S*1 and *S*2, respectively. The string lengths of both strings are no more than 104. It is guaranteed that all the characters are visible ASCII codes and white space, and a new line character signals the end of a string.

### Output Specification:

For each test case, print *S*1−*S*2 in one line.

### Sample Input:

```in
They are students.
aeiou
```

### Sample Output:

```out
Thy r stdnts.
```

#### Idea

对 $S_2$ 进行判重,使得 $S_2$ 最长只有256位

### AC code

#### 朴素做法(PAT也可以过)

```cpp
#include <iostream>

using namespace std;

string s1, s2;

bool check_exists(char c){// 该循环可以进行化简,从O(n)到O(1) 
    for(auto a : s2){// 该函数的作用就是判断一个元素是否在某个集合中出现过串中出现过
        if(a == c) return true;
    }// 可以使用hash表进行优化,hash表可以将增删改查做到O(1)的复杂度
    return false;
}

int main(void){
    
    getline(cin, s1);
    getline(cin, s2);
    
    string res;
    for(auto c : s1){// 该循环无法避免
        if(!check_exists(c)) res += c;
    }
    
    cout << res << endl;
    
    return 0;
}
```

#### Hash优化

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

string s1, s2;

int main(void){

    getline(cin, s1);
    getline(cin, s2);

    unordered_set<char> hash;// 定义hash表
    for(auto c : s2) hash.insert(c);// 插入hash表


    string ans;
    for(auto c : s1){
        if(!hash.count(c)) ans += c;
        // 该函数会统计hash表中该元素的个数
    }

    cout << ans << endl;

    return 0;
}
```


*2022-07-17 周日*