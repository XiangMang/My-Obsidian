## [题目详情 - 1009 Product of Polynomials (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805509540921344)

[1481. 多项式乘积 - AcWing题库](https://www.acwing.com/problem/content/1483/)

#简单

This time, you are supposed to find $A×B$ where $A$ and $B$ are two polynomials.

### Input Specification:

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial:

$K ~N_1 ~a_{N_1} ~N_2 ~a_{N_2} ~... ~N_K ~a_{N_K}$

where K is the number of nonzero terms in the polynomial, $N_i$ and $a_{N_i} (i=1,2,⋯,K)$ are the exponents and coefficients, respectively. It is given that $1 \leq K \leq 10,0 \leq N_K< \dots <N_2<N_1 \leq 1000$.

### Output Specification:

For each test case you should output the product[^1] of $A$ and $B$ in one line, with the same format as the input. Notice that there must be **NO** extra space at the end of each line. Please be accurate up to 1 decimal place.

### Sample Input:

```in
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```

### Sample Output:

```out
3 3 3.6 2 6.0 1 1.6
```

### AC code

```cpp
#include <iostream>

using namespace std;

const int N = 1e3 + 10;

int n, m;
double a[N], b[N], c[2 * N];

int main(void){

    cin >> n;
    while(n--){
        int i;
        double j;
        cin >> i >> j;
        a[i] = j;
    }

    cin >> m;
    while(m--){
        int i;
        double j;
        cin >> i >> j;
        b[i] = j;
    }

    for(int i = N; i >= 0; i--){
        for(int j = N; j >= 0; j--){
            c[i + j] += a[i] * b[j];
        }
    }

    int k = 0; 
    for(auto s : c) if(s != 0) k++;
    printf("%d", k);
    for(int i = 2 * N; i >= 0; i--){
        if(c[i] != 0){
            printf(" %d %.1lf", i, c[i]);
        }
    }

    return 0;
}
```


*2022-07-19 周二*

[^1]: product $n.$ 乘积