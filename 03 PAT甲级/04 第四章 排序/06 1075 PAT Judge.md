## [题目详情 - 1075 PAT Judge (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805393241260032)

[1561. PAT 评测 - AcWing题库](https://www.acwing.com/problem/content/1563/)

#排序 #构造函数 #unordered_map #c-str #vector 

The ranklist of PAT is generated from the status list, which shows the scores of the submissions. This time you are supposed to generate the ranklist for PAT.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 3 positive integers, $N (≤10^4)$, the total number of users,$ K (≤5)$, the total number of problems, and $M (≤10^5)$, the total number of submissions. It is then assumed that the user id's are 5-digit numbers from 00001 to $N$, and the problem id's are from $1$ to $K$. The next line contains $K$ positive integers `p[i]` $(i=1, ..., K)$, where `p[i]` corresponds to the full mark of the i-th problem. Then M lines follow, each gives the information of a submission in the following format:

```
user_id problem_id partial_score_obtained
```

where `partial_score_obtained` is either $−1$ if the submission cannot even pass the compiler, or is an integer in the range $[0, p[problem_id]]$. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, you are supposed to output the ranklist in the following format:

```
rank user_id total_score s[1] ... s[K]
```

where `rank` is calculated according to the `total_score`, and all the users with the same `total_score` obtain the same `rank`; and `s[i]` is the partial score obtained for the `i`-th problem. If a user has never submitted a solution for a problem, then "-" must be printed at the corresponding position. If a user has submitted several solutions to solve one problem, then the highest score will be counted.

The ranklist must be printed in non-decreasing order of the ranks. For those who have the same rank, users must be sorted in nonincreasing order according to the number of perfectly solved problems. And if there is still a tie, then they must be printed in increasing order of their id's. For those who has never submitted any solution that can pass the compiler, or has never submitted any solution, they must NOT be shown on the ranklist. It is guaranteed that at least one user can be shown on the ranklist.

### Sample Input:

```in
7 4 20
20 25 25 30
00002 2 12
00007 4 17
00005 1 19
00007 2 25
00005 1 20
00002 2 2
00005 1 15
00001 1 18
00004 3 25
00002 2 25
00005 3 22
00006 4 -1
00001 2 18
00002 1 20
00004 1 15
00002 4 18
00001 3 4
00001 4 2
00005 2 -1
00004 2 0
```

### Sample Output:

```out
1 00002 63 20 25 - 18
2 00005 42 20 0 22 -
2 00007 42 - 25 - 17
2 00001 42 18 18 4 2
5 00004 40 15 0 25 -
```

### Idea

1. 使用结构体对学生的信息进行存储
2. 注意学生的排序顺序
3. 使用hash表进行映射

### AC code

#### STL

```cpp
#include <iostream>
#include <algorithm>
#include <unordered_map>
#include <vector>//对所有同学的成绩进行排序

using namespace std;

const int K = 6;

int n, k, m;
int p_score[K];

struct Student{
    string id;
    int grade[K];
    int total, cnt;

    Student(){}// 构造函数
    Student(string _id) : id(_id){// 对题目分数进行初始化
        for(int i = 1; i <= k; i++) grade[i] = -2;// -2代表没有提交
        total = 0;
        cnt = 0;
    }

    void calc(void){// 计算函数
        for(int i = 1; i <= k; i++){
            total += max(0, grade[i]);// 总分
            if(grade[i] == p_score[i]) cnt++;//满分的数量
        }
    }

    bool has_submit(void){
        for(int i = 1; i <= k; i++){
            if(grade[i] >= 0) return true;
        }
        return false;
    }

    bool operator< (const Student& t) const{
        if(total != t.total) return total > t.total;
        if(cnt != t.cnt) return cnt > t.cnt;
        return id < t.id;
    }
};

int main(void){

    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    unordered_map<string, Student> students;

    cin >> n >> k >> m;
    for(int i = 1; i <= k; i++) cin >> p_score[i];

    while(m--){
        string user_id;
        int p_id, grade;
        cin >> user_id >> p_id >> grade;

        if(students.count(user_id) == 0) students[user_id] = Student(user_id);
        // 如果当然人名不存在就进行初始化操作
        students[user_id].grade[p_id] = max(students[user_id].grade[p_id], grade);
        // 读入成绩
    }

    vector<Student> res;
    for(auto& item : students){
        auto& s = item.second;
        if(s.has_submit()){
            s.calc();
            res.push_back(s);
        }
    }

    sort(res.begin(), res.end());

    for (int i = 0, rank = 1; i < res.size(); i++){
        if (i && res[i].total != res[i - 1].total) rank = i + 1;
        cout << rank << ' ' << res[i].id << ' ' << res[i].total;
        for (int j = 1; j <= k; j++){
            if (res[i].grade[j] == -2) cout << " -";
            else cout << ' ' << max(0, res[i].grade[j]);
        }  
        cout << endl;
    }

    return 0;
}
```

#### char

```cpp
#include <iostream>
#include <algorithm>
#include <unordered_map>
#include <vector>

using namespace std;

const int K = 6;

int n, k, m;
int p_score[K];

struct Student{
    string id;
    int grade[K];
    int total, cnt;

    Student(){}
    Student(string _id) : id(_id){
        for (int i = 1; i <= k; i ++ ) grade[i] = -2;
        total = cnt = 0;
    }

    void calc(){
        for (int i = 1; i <= k; i ++ )
        {
            total += max(0, grade[i]);
            if (grade[i] == p_score[i]) cnt ++ ;
        }
    }

    bool has_submit(){
        for (int i = 1; i <= k; i ++ )
            if (grade[i] >= 0)
                return true;
        return false;
    }

    bool operator< (const Student& t) const{
        if (total != t.total) return total > t.total;
        if (cnt != t.cnt) return cnt > t.cnt;
        return id < t.id;
    }
};

int main(void){

    unordered_map<string, Student> students;

    scanf("%d%d%d", &n, &k, &m);
    for (int i = 1; i <= k; i ++ ) scanf("%d", &p_score[i]);

    while (m -- ){
        string u_id;
        char u_id_s[6];
        int p_id, grade;
        scanf("%s%d%d", u_id_s, &p_id, &grade);
        u_id = u_id_s;

        if (students.count(u_id) == 0) students[u_id] = Student(u_id);
        students[u_id].grade[p_id] = max(students[u_id].grade[p_id], grade);
    }

    vector<Student> res;
    for (auto& item: students){
        auto& s = item.second;
        if (s.has_submit())
        {
            s.calc();
            res.push_back(s);
        }
    }

    sort(res.begin(), res.end());

    for (int i = 0, rank = 1; i < res.size(); i ++ ){
        if (i && res[i].total != res[i - 1].total) rank = i + 1;
        printf("%d %s %d", rank, res[i].id.c_str(), res[i].total);
        for (int j = 1; j <= k; j ++ )
            if (res[i].grade[j] == -2) printf(" -");
            else printf(" %d", max(0, res[i].grade[j]));
        puts("");
    }

    return 0;
}
```

相关文章:[[C++结构体的构造函数]]

*2022-07-28 周四*