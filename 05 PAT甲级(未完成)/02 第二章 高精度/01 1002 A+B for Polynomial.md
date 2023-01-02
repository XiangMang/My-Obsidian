## [题目详情 - 1002 A+B for Polynomials (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805526272000000)

[1474. 多项式 A + B - AcWing题库](https://www.acwing.com/problem/content/1476/)

#简单 

This time, you are supposed to find $A+B$ where $A$ and $B$ are two polynomials[^1].

### Input Specification:

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial:

$K ~N_1 ~a_{N_1} ~N_2 ~a_{N_2} ~... ~N_K ~a_{N_K}$

where $K$ is the number of nonzero terms[^2] in the polynomial, $N_i$ and $a_{N_i} (i=1,2,⋯,K)$ are the exponents[^3] and coefficients[^4], respectively. It is given that $1≤K≤10，0≤N_K<⋯<N_2<N_1≤1000$.

### Output Specification:

For each test case you should output the sum of $A$ and $B$ in one line, with the same format as the input. Notice that there must be **NO** extra space at the end of each line. Please be accurate[^5] to 1 decimal[^6] place.

### Sample Input:

```in
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```

### Sample Output:

```out
3 2 1.5 1 2.9 0 3.2
```

### AC code

```cpp
#include <iostream>

using namespace std;

const int N = 1010;

int n, m;
double no[N];

int main(void){

    cin >> n;
    while(n--){
        int a;
        double b;
        cin >> a >> b;
        no[a] += b;
    }

    cin >> m;
    while(m--){
        int a;
        double b;
        cin >> a >> b;
        no[a] += b;
    }

    int k = 0;
    for(auto c : no) if(c != 0) k++;
    printf("%d", k);
    for(int i = 1000; i >= 0; i--){
        if(no[i] != 0) printf(" %d %.1lf", i, no[i]);
    }

    return 0;
}
```


*2022-07-19 周二*

[^1]: polynomials $n.$ 多项式
[^2]: term $n.$ (数学运算中的)项
[^3]: exponent $n.$ 幂
[^4]: coefficient $n.$ 系数
[^5]: accurate $adj.$ 精确的
[^6]: decimal $adj.$ 小数的