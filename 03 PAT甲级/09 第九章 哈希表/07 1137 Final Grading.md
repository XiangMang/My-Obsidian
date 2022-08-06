## [题目详情 - 1137 Final Grading (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805345401028608)

[1630. 期终成绩 - AcWing题库](https://www.acwing.com/problem/content/1632/)

#hash #排序 #构造函数 #unordered_map #c-str #vector 

For a student taking the online course "Data Structures" on China University MOOC (http://www.icourse163.org/), to be qualified for a certificate, he/she must first obtain no less than 200 points from the online programming assignments, and then receive a final grade no less than 60 out of 100. The final grade is calculated by $G=(G_{mid−term}×40\%+G_{final}×60\%)$ if $G_{mid−term}>G_{final}$, or $G_{final}$ will be taken as the final grade $G$. Here $G_{mid−term}$ and $G_{final}$ are the student's scores of the mid-term and the final exams, respectively.

The problem is that different exams have different grading sheets. Your job is to write a program to merge all the grading sheets into one.

### Input Specification:

Each input file contains one test case. For each case, the first line gives three positive integers: P , the number of students having done the online programming assignments; M, the number of students on the mid-term list; and N, the number of students on the final exam list. All the numbers are no more than 10,000.

Then three blocks follow. The first block contains P online programming scores $G_p$'s; the second one contains M mid-term scores $G_{mid−term}$'s; and the last one contains N final exam scores $G_{final}$'s. Each score occupies a line with the format: `StudentID Score`, where `StudentID` is a string of no more than 20 English letters and digits, and `Score` is a nonnegative integer (the maximum score of the online programming is 900, and that of the mid-term and final exams is 100).

### Output Specification:

For each case, print the list of students who are qualified for certificates. Each student occupies a line with the format:

`StudentID` $G_p ~G_{mid−term} ~G_{final} ~G$

If some score does not exist, output "−1" instead. The output must be sorted in descending order of their final grades ($G$ must be rounded up to an integer). If there is a tie, output in ascending order of their `StudentID`'s. It is guaranteed that the `StudentID`'s are all distinct, and there is at least one qullified student.

### Sample Input:

```in
6 6 7
01234 880
a1903 199
ydjh2 200
wehu8 300
dx86w 220
missing 400
ydhfu77 99
wehu8 55
ydjh2 98
dx86w 88
a1903 86
01234 39
ydhfu77 88
a1903 66
01234 58
wehu8 84
ydjh2 82
missing 99
dx86w 81
```

### Sample Output:

```out
missing 400 -1 99 99
ydjh2 200 98 82 88
dx86w 220 88 81 84
wehu8 300 55 84 84
```

### Idea

- 如果某位同学没有成绩,就标注为 `-1`
- 使用 `unordered_map` 从 `string`  映射到结构体

### AC code

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <unordered_map>
#include <cmath>

using namespace std;

struct Student{
    string id;
    int p, m, f, s;

    Student(): p(-1), m(-1), f(-1), s(-1){}

    void calc(void){
        if(f >= m) s = f;
        else s = round(0.4 * m + 0.6 * f);
    }

    bool operator< (const Student& t) const{
        if(s != t.s) return s > t.s;
        return id < t.id;
    }
};

int main(void){

    int p, m, n;
    cin >> p >> m >> n;

    unordered_map<string, Student> hash;
    string id;
    int s;

    for(int i = 0; i < p; i++){
        cin >> id >> s;
        hash[id].id = id;
        hash[id].p = s;
    }

    for(int i = 0; i < m; i++){
        cin >> id >> s;
        hash[id].id = id;
        hash[id].m = s;
    }

    for(int i = 0; i < n; i++){
        cin >> id >> s;
        hash[id].id = id;
        hash[id].f = s;
    }

    vector<Student> student;
    for(auto item : hash){
        auto stu = item.second;
        stu.calc();
        if(stu.p >= 200 && stu.s >= 60) student.push_back(stu);
    }

    sort(student.begin(), student.end());

    for(auto item : student){
        cout << item.id << ' ' << item.p << ' ' << item.m << ' ' << item.f << ' ' << item.s << endl;
    }

    return 0;
}
```


相关题目:
1. [[06 1075 PAT Judge]]

*2022-08-06 周六*