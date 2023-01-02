## [题目详情 - 1103 Integer Factorization (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/994805364711604224)

[1593. 整数分解 - AcWing题库](https://www.acwing.com/problem/content/1595/)

The $K-P$ factorization of a positive integer $N$ is to write $N$ as the sum of the $P$-th power of $K$ positive integers. You are supposed to write a program to find the $K-P$ factorization of $N$ for any positive integers $N$, $K$ and $P$.

### Input Specification:

Each input file contains one test case which gives in a line the three positive integers $N ( \leq 400), K ( \leq N)$ and $P (1<$P$ \leq 7)$. The numbers in a line are separated by a space.

### Output Specification:

For each case, if the solution exists, output in the format:

```
N = n[1]^P + ... n[K]^P
```

where `n[i]` (`i` = 1, ..., `K`) is the `i`-th factor. All the factors must be printed in non-increasing order.

Note: the solution may not be unique. For example, the 5-2 factorization of 169 has 9 solutions, such as $12^2+4^2+2^2+2^2+1^2$, or $11^2+6^2+2^2+2^2+2^2$, or more. You must output the one with the maximum sum of the factors. If there is a tie, the largest factor sequence must be chosen -- sequence { $a_1,a_2, \dots,a_K$ } is said to be **larger** than { $b_1,b_2, \dots,b_K$ } if there exists $1 \leq L \leq K$ such that $a_i=b_i$ for $i<L$ and $a_L>b_L$.

If there is no solution, simple output `Impossible`.

### Sample Input 1:

```in
169 5 2
```

### Sample Output 1:

```out
169 = 6^2 + 6^2 + 6^2 + 6^2 + 5^2
```

### Sample Input 2:

```in
169 167 3
```

### Sample Output 2:

```out
Impossible
```

### Idea



### AC code

```cpp
```


*2023-01-01 周日*