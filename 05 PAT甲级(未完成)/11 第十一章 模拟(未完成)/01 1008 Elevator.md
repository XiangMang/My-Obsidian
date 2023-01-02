## [题目详情 - 1008 Elevator (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805511923286016)

[1480. 电梯 - AcWing题库](https://www.acwing.com/problem/content/1482/)

#简单 

The highest building in our city has only one elevator. A request list is made up with $N$ positive numbers. The numbers denote at which floors the elevator will stop, in specified order. It costs 6 seconds to move the elevator up one floor, and 4 seconds to move down one floor. The elevator will stay for 5 seconds at each stop.

For a given request list, you are to compute the total time spent to fulfill the requests on the list. The elevator is on the 0th floor at the beginning and does not have to return to the ground floor when the requests are fulfilled.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer $N$, followed by $N$ positive numbers. All the numbers in the input are less than 100.

### Output Specification:

For each test case, print the total time on a single line.

### Sample Input:

```in
3 2 3 1
```

### Sample Output:

```out
41
```

### AC code

```cpp
#include <iostream>

using namespace std;

const int N = 110;

int n;
int q[N];
int ans;

int main(void){

    cin >> n;
    for(int i = 1; i <= n; i++) cin >> q[i];

    for(int i = 1; i <= n; i++){
        if(q[i] > q[i - 1]) ans += (q[i] - q[i - 1]) * 6 + 5;
        else if(q[i] == q[i - 1]) ans += 5;
        else ans += (q[i - 1] - q[i]) * 4 + 5;
    }

    cout << ans << endl;

    return 0;
}
```


*2022-08-07 周日*