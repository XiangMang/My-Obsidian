## [题目详情 - 1036 Boys vs Girls (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805453203030016)

[1520. 男孩 vs 女孩 - AcWing题库](https://www.acwing.com/problem/content/1522/)

#简单 #字符串 #模拟

This time you are asked to tell the difference between the lowest grade of all the male students and the highest grade of all the female students.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer *N*, followed by *N* lines of student information. Each line contains a student's `name`, `gender`, `ID` and `grade`, separated by a space, where `name` and `ID` are strings of no more than 10 characters with no space, `gender` is either `F` (female) or `M` (male), and `grade` is an integer between 0 and 100. It is guaranteed that all the grades are distinct[^1].

### Output Specification:

For each test case, output in 3 lines. The first line gives the name and ID of the female student with the highest grade, and the second line gives that of the male student with the lowest grade. The third line gives the difference $grade_F−grade_M$[^2]. If one such kind of student is missing, output `Absent` in the corresponding line, and output `NA` in the third line instead.

### Sample Input 1:

```in
3
Joe M Math990112 89
Mike M CS991301 100
Mary F EE990830 95
```

### Sample Output 1:

```out
Mary EE990830
Joe Math990112
6
```

### Sample Input 2:

```in
1
Jean M AA980920 60
```

### Sample Output 2:

```out
Absent
Jean AA980920
NA
```

### Idea

主要就是分析出变量的设置

### AC code

```cpp
#include <iostream>

using namespace std;

int main(void){

    int n;
    cin >> n;

    string f_name, f_id;
    string m_name, m_id;
    int f_score, m_score;

    for(int i = 0; i < n; i++){
        string name, id, sex;
        int score;
        cin >> name >> sex >> id >> score;
        if(sex == "M"){
            if(m_name.empty() || m_score > score){
                m_name = name;
                m_id = id;
                m_score = score;
            }
        }
        else{
            if(f_name.empty() || f_score < score){
                f_name = name;
                f_id = id;
                f_score = score;
            }
            }
    }

    if(f_name.empty()) puts("Absent");
    else cout << f_name << " " << f_id << endl;
    if(m_name.empty()) puts("Absent");
    else cout << m_name << " " << m_id << endl;
    if(m_name.size() && f_name.size()) cout << abs(m_score - f_score) << endl;
    // 如果男女生存在的话,那么size就不为零,故可以这样判断
    else puts("NA");

    return 0;
}
```


*2022-07-14 周四*

[^1]: distinct $adj.$ 不同的
[^2]: 此处需要使用绝对值函数