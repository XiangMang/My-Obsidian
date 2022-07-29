## [题目详情 - 1028 List Sorting (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805468327690240)

[1505. 列表排序 - AcWing题库](https://www.acwing.com/problem/content/1507/)

#c-str #排序 #vector 

Excel can sort records according to any column. Now you are supposed to imitate this function.

### Input Specification:

Each input file contains one test case. For each case, the first line contains two integers $N (≤10^5)$ and $C$, where N is the number of records and $C$ is the column that you are supposed to sort the records with. Then $N$ lines follow, each contains a record of a student. A student's record consists of his or her distinct ID (a 6-digit number), name (a string with no more than 8 characters without space), and grade (an integer between 0 and 100, inclusive).

### Output Specification:

For each test case, output the sorting result in N lines. That is, if $C$ = 1 then the records must be sorted in increasing order according to ID's; if $C$ = 2 then the records must be sorted in non-decreasing order according to names; and if $C$ = 3 then the records must be sorted in non-decreasing order according to grades. If there are several students who have the same name or grade, they must be sorted according to their ID's in increasing order.

### Sample Input 1:

```in
3 1
000007 James 85
000010 Amy 90
000001 Zoe 60
```

### Sample Output 1:

```out
000001 Zoe 60
000007 James 85
000010 Amy 90
```

### Sample Input 2:

```in
4 2
000007 James 85
000010 Amy 90
000001 Zoe 60
000002 James 98
```

### Sample Output 2:

```out
000010 Amy 90
000002 James 98
000007 James 85
000001 Zoe 60
```

### Sample Input 3:

```in
4 3
000007 James 85
000010 Amy 90
000001 Zoe 60
000002 James 9
```

### Sample Output 3:

```out
000002 James 9
000001 Zoe 60
000007 James 85
000010 Amy 90
```

### Idea 

不使用 `operator` 使用`cmp比较函数`

### AC code

#### STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Info{
    string id, name;
    int grade;
};

vector<Info> info;

bool cmp1(Info a, Info b){
    return a.id < b.id;
}

bool cmp2(Info a, Info b){
    if(a.name != b.name) return a.name < b.name;
    return a.id < b.id;
}

bool cmp3(Info a, Info b){
    if(a.grade != b.grade) return a.grade < b.grade;
    return a.id < b.id;
}

int main(void){

    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    // 以上三行代码用来打消iostream的输入 输出缓存

    int n, m;
    cin >> n >> m;

    while(n--){
        string id, name;
        int grade;
        cin >> id >> name >> grade;
        info.push_back({id, name, grade});
    }
    
    if(m == 1) sort(info.begin(), info.end(), cmp1);
    else if(m == 2) sort(info.begin(), info.end(), cmp2);
    else sort(info.begin(), info.end(), cmp3);

    for(auto& item : info){
        cout << item.id << ' ' << item.name << ' ' << item.grade << endl;
    }

    return 0;
}
```

#### 数组

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100010;

int n;

struct Row{
    string id, name;
    int grade;
}rows[N];

bool cmp1(Row a, Row b){
    return a.id < b.id;
}

bool cmp2(Row a, Row b){
    if (a.name != b.name) return a.name < b.name;
    return a.id < b.id;
}

bool cmp3(Row a, Row b){
    if (a.grade != b.grade) return a.grade < b.grade;
    return a.id < b.id;
}

int main(void){

    int c;
    scanf("%d%d", &n, &c);
    char id[10], name[10];// 使用char作为中间转换
    for (int i = 0; i < n; i ++ ){
        int grade;
        scanf("%s%s%d", id, name, &grade);
        rows[i] = {id, name, grade};
    }

    if (c == 1) sort(rows, rows + n, cmp1);
    else if (c == 2) sort(rows, rows + n, cmp2);
    else sort(rows, rows + n, cmp3);

    for (int i = 0; i < n; i ++ ){
        printf("%s %s %d\n", rows[i].id.c_str(), rows[i].name.c_str(), rows[i].grade);
    }
    
    return 0;
}
```


相关文章:[[升序，降序，非升序，非降序]]

*2022-07-26 周二*