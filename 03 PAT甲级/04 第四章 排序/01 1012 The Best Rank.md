## [题目详情 - 1012 The Best Rank (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805502658068480)

[1484. 最佳排名 - AcWing题库](https://www.acwing.com/problem/content/1486/)

#hash #二分 #unordered_map #排序

To evaluate the performance of our first year CS majored students, we consider their grades of three courses only: `C` - C Programming Language, `M` - Mathematics (Calculus or Linear Algrbra), and `E` - English. At the mean time, we encourage students by emphasizing on their best ranks -- that is, among the four ranks with respect to the three courses and the average grade, we print the best rank for each student.

For example, The grades of `C`, `M`, `E` and `A` - Average of 4 students are given as the following:

```
StudentID  C  M  E  A
310101     98 85 88 90
310102     70 95 88 84
310103     82 87 94 88
310104     91 91 91 91
```

Then the best ranks for all the students are No.1 since the 1st one has done the best in C Programming Language, while the 2nd one in Mathematics, the 3rd one in English, and the last one in average.

### Input Specification:

Each input file contains one test case. Each case starts with a line containing 2 numbers $N$ and $M (≤2000)$, which are the total number of students, and the number of students who would check their ranks, respectively. Then $N$ lines follow, each contains a student ID which is a string of 6 digits, followed by the three integer grades (in the range of [0, 100]) of that student in the order of `C`, `M` and `E`. Then there are $M$ lines, each containing a student ID.

### Output Specification:

For each of the $M$ students, print in one line the best rank for him/her, and the symbol of the corresponding rank, separated by a space.

The priorities of the ranking methods are ordered as `A` > `C` > `M` > `E`. Hence if there are two or more ways for a student to obtain the same best rank, output the one with the highest priority.

If a student is not on the grading list, simply output `N/A`.

### Sample Input:

```in
5 6
310101 98 85 88
310102 70 95 88
310103 82 87 94
310104 91 91 91
310105 85 90 90
310101
310102
310103
310104
310105
999999
```

### Sample Output:

```out
1 C
1 M
1 E
1 A
3 A
N/A
```

### Idea

1. 使用 `round()` 处理四舍五入
2. 使用 `map` 记录每个人的信息
3. 使用 `vector + 数组` 存储每个科目的分数

### AC code

```cpp
#include <iostream>
#include <unordered_map>
#include <cmath>
#include <vector>
#include <algorithm>

using namespace std;

unordered_map<string, vector<int>> grades;
vector<int> q[4];  // A: q[0], C: q[1], M: q[2], E: q[3]

int get_rank(vector<int>& a, int x){
    int l = 0, r = a.size() - 1;
    while(l < r){// 此处必须用 <=
        int mid = l + r + 1>> 1;
        if(a[mid] <= x) l = mid;
        else r = mid - 1;
    }
    return a.size() - l;
}

int main(void){

    int n, m;
    cin >> n >> m;

    for(int i = 0; i < n; i++){
        string id;
        int t[4] = {0};
        cin >> id;
        for(int i = 1; i < 4; i++){
            cin >> t[i];
            t[0] += t[i];
        }
        t[0] = round(t[0] / 3.0);
        // 四舍五入函数

        for(int j = 0; j < 4; j++){
            q[j].push_back(t[j]);// 将成绩按照科目进行划分
            grades[id].push_back(t[j]);// 将成绩按照任务进行划分
        }
    }

    for(int i = 0; i < 4; i++) sort(q[i].begin(), q[i].end());
    // 对各科成绩进行排序

    char names[] = "ACME";
    while(m--){
        string id;
        cin >> id;
        if(grades.count(id) == 0) puts("N/A");// 通过hash表中的count判断是否存在
        else{
            int res = n + 1;// 排名
            char c;// 科目
            for(int i = 0; i < 4; i++){// 对每个分数进行排序,同时确定了优先级
                int rank = get_rank(q[i], grades[id][i]);
                if(rank < res){
                    res = rank;
                    c = names[i];
                }
            }
            cout << res << ' ' << c << endl;
        }
    }

    return 0;
}
```
相关文章:
1. [[关于二分模板的使用]]


*2022-07-20 周三*