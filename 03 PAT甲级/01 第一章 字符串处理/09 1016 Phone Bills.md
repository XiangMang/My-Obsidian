## [题目详情 - 1016 Phone Bills (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805493648703488)

[1493. 电话账单 - AcWing题库](https://www.acwing.com/problem/content/1495/)

#模拟 #operator #字符串 #c-str 

A long-distance telephone company charges its customers by the following rules:

Making a long-distance call costs a certain amount per minute, depending on the time of day when the call is made. When a customer starts connecting a long-distance call, the time will be recorded, and so will be the time when the customer hangs up the phone. Every calendar month, a bill is sent to the customer for each minute called (at a rate determined by the time of day). Your job is to prepare the bills for each month, given a set of phone call records.

### Input Specification:

Each input file contains one test case. Each case has two parts: the rate structure, and the phone call records.

The rate structure consists of a line with 24 non-negative integers denoting the toll (cents/minute) from 00:00 - 01:00, the toll from 01:00 - 02:00, and so on for each hour in the day.

The next line contains a positive number *N* (≤1000), followed by *N* lines of records. Each phone call record consists of the name of the customer (string of up to 20 characters without space), the time and date (`MM:dd:HH:mm`), and the word `on-line` or `off-line`.

For each test case, all dates will be within a single month. Each `on-line` record is paired with the chronologically next record for the same customer provided it is an `off-line` record. Any `on-line` records that are not paired with an `off-line` record are ignored, as are `off-line` records not paired with an `on-line` record. It is guaranteed that at least one call is well paired in the input. You may assume that no two records for the same customer have the same time. Times are recorded using a 24-hour clock.

### Output Specification:

For each test case, you must print a phone bill for each customer.

Bills must be printed in alphabetical order of customers' names. For each customer, first print in a line the name of the customer and the month of the bill in the format shown by the sample. Then for each time period of a call, print in one line the beginning and ending time and date (`dd:HH:mm`), the lasting time (in minute) and the charge of the call. The calls must be listed in chronological order. Finally, print the total charge for the month in the format shown by the sample.

### Sample Input:

```in
10 10 10 10 10 10 20 20 20 15 15 15 15 15 15 15 20 30 20 15 15 10 10 10
10
CYLL 01:01:06:01 on-line
CYLL 01:28:16:05 off-line
CYJJ 01:01:07:00 off-line
CYLL 01:01:08:03 off-line
CYJJ 01:01:05:59 on-line
aaa 01:01:01:03 on-line
aaa 01:02:00:01 on-line
CYLL 01:28:15:41 on-line
aaa 01:05:02:24 on-line
aaa 01:04:23:59 off-line
```

### Sample Output:

```out
CYJJ 01
01:05:59 01:07:00 61 $12.10
Total amount: $12.10
CYLL 01
01:06:01 01:08:03 122 $24.40
28:15:41 28:16:05 24 $3.85
Total amount: $28.25
aaa 01
02:00:01 04:23:59 4318 $638.80
Total amount: $638.80
```

### Idea

1. 将所有时间段的花费存储在数组中,否则如果使用每过一秒就算一次花费,在极端情况下,需要计算 `31*24*60*24`次,故使用前缀和进行优化(每次都是计算每一个区间的花费是多少)
2. 使用结构体将客户的姓名,时间,当时的状态作为记录
3.  使用 `map` 进行存储
4. 设置一个格式化时间,用来存储当时的时间距离当月一月一号的时间

### AC Code

```cpp
#include <map>
#include <vector>
#include <cstdio>
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1010, M = 31 * 1440 + 10;

int n;
int cost[24];  // 每个时间段的花费
double sum[M];  // 从当月1号00:00开始到每个时刻所花费的分钟数

struct Record{
    int minutes;
    string state;
    string format_time;

    bool operator< (const Record& t) const{
        return minutes < t.minutes;
    }
};

map<string, vector<Record>> persons;  // string存姓名，vector存信息

int main(void){

    for(int i = 0; i < 24; i++) cin >> cost[i];
    for(int i = 1; i < M; i++) sum[i] = sum[i - 1] + cost[(i - 1) % 1440 / 60] / 100.0;
    // 如果单独计算每一分钟的花费，时间复杂度太高，故用前缀和优化
    // 如果电话从月初一直拨打到月末，则复杂度为 31 * 1440 * 24
    // cost表示i - 1时刻在那一天的哪一个时间段，并换算成美元

    cin >> n;
    int month, day, hour, minute;
    char name[25], state[25], format_time[25];

    for(int i = 0; i < n; i++){
        scanf("%s %d:%d:%d:%d %s", name, &month, &day, &hour, &minute, state);
        sprintf(format_time, "%02d:%02d:%02d", day, hour, minute);
        // C 库函数 int sprintf(char *str, const char *format, ...) 发送格式化输出到 str 所指向的字符串
        // int sprintf(char *str, const char *format, ...) <cstdio>

        int minutes = (day - 1) * 1440 + hour * 60 + minute;
        persons[name].push_back({minutes, state, format_time});
    }

    for(auto &person : persons){
        auto name = person.first;
        auto records = person.second;  // 就是map中的vector
        sort(records.begin(), records.end());  // 按照时间排序

        double total = 0;
        for(int i = 0; i + 1 < records.size(); i++){
            auto a = records[i], b = records[i + 1];
            if(a.state == "on-line" && b.state == "off-line"){
                if(!total) printf("%s %02d\n", name.c_str(), month);  // 判断是否是第一次输入
                // c_str将string型转为char型
                cout << a.format_time << ' ' << b.format_time;

                double c = sum[b.minutes] - sum[a.minutes];
                printf(" %d $%.2lf\n", b.minutes - a.minutes, c);
                total += c;
            }
        }

        if (total) printf("Total amount: $%.2lf\n", total);
    }

    return 0;
}
```

*2022-07-19 周二*