## [题目详情 - 1025 PAT Ranking (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805474338127872)

[1502. PAT 排名 - AcWing题库](https://www.acwing.com/problem/content/1504/)

#operator #排序 #vector 

Programming Ability Test (PAT) is organized by the College of Computer Science and Technology of Zhejiang University. Each test is supposed to run simultaneously[^1] in several[^2] places, and the ranklists[^3] will be merged immediately[^4] after the test. Now it is your job to write a program to correctly[^5] merge all the ranklists and generate[^6] the final rank.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive number $N (≤100)$, the number of test locations[^7]. Then $N$ ranklists follow, each starts with a line containing a positive integer $K (≤300)$, the number of testees, and then $K$ lines containing the registration number (a 13-digit number) and the total score of each testee. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, first print in one line the total number of testees. Then print the final ranklist in the following format:

```
registration_number final_rank location_number local_rank
```

The locations are numbered from 1 to $N$. The output must be sorted in nondecreasing order of the final ranks. The testees with the same score must have the same rank, and the output must be sorted in nondecreasing order of their registration[^8] numbers.

### Sample Input:

```in
2
5
1234567890001 95
1234567890005 100
1234567890003 95
1234567890002 77
1234567890004 85
4
1234567890013 65
1234567890011 25
1234567890014 100
1234567890012 85
```

### Sample Output:

```out
9
1234567890005 1 1 1
1234567890014 1 2 1
1234567890001 3 1 2
1234567890003 3 1 2
1234567890004 5 1 4
1234567890012 5 2 2
1234567890002 7 1 5
1234567890013 8 2 3
1234567890011 9 2 4
```

### Idea

1. 将信息分两份存储,一份是地区,一份是全国
2. 以分数作为第一关键字,以考号作为第二关键字
3. 如果当前的考生分数与前一个不相同,就在之前的基础上加一

### AC code

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

const int N = 110;

struct Student{
    string id;
    int grade;
    int location_number, local_rank, final_rank;

    bool operator< (const Student& t) const{// 首先判断分数是否相同,如果相同就判断考号
        if(grade != t.grade) return grade > t.grade;// 分高的在前
        return id < t.id;// 考号小的先输出
    }
};

vector<Student> grades[N];
vector<Student> all;
// 将考生信息分两份存储

int main(void){

    int n;
    cin >> n;

    for(int i = 1; i <= n; i++){
        int k;
        cin >> k;
        for(int j = 0; j < k; j++){
            string id;
            int grade;
            cin >> id >> grade;
            grades[i].push_back({id, grade, i});
            // 读入考生的id,分数,地区
        }
        
        auto& g = grades[i];
        sort(g.begin(), g.end());
        for(int j = 0; j < g.size(); j++){
            if(!j || g[j].grade != g[j - 1].grade) g[j].local_rank = j + 1;
            else g[j].local_rank = g[j - 1].local_rank;
            all.push_back(g[j]);
        }
    }

    sort(all.begin(), all.end());
    for(int i = 0; i < all.size();i++){
        if(!i || all[i].grade != all[i - 1].grade) all[i].final_rank = i + 1;
        else all[i].final_rank = all[i - 1].final_rank;
    }
    
    cout << all.size() << endl;
    for(auto& item : all){
        cout << item.id << ' ' << item.final_rank << ' ' << item.location_number << ' ' << item.local_rank << endl;
    }

    return 0;
}
```


*2022-07-26 周二*

[^1]:  simultaneously $adv.$ 同时的
[^2]: several $adj.$ 不同的
[^3]: ranklist 排名表
[^4]: immediatel $adv.$ 立即
[^5]: correctly $adv.$ 正确的
[^6]: generate $v.$ 产生
[^7]: location $n.$ 地点
[^8]: registration $n.$ 登记