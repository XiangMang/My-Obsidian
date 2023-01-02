## [题目详情 - 1088 Rational Arithmetic (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/994805378443755520)

[1578. 有理数运算 - AcWing题库](https://www.acwing.com/problem/content/1580/)

For two rational numbers, your task is to implement the basic arithmetics, that is, to calculate their sum, difference, product and quotient.

### Input Specification:

Each input file contains one test case, which gives in one line the two rational numbers in the format `a1/b1 a2/b2`. The numerators and the denominators are all in the range of long int. If there is a negative sign, it must appear only in front of the numerator. The denominators are guaranteed to be non-zero numbers.

### Output Specification:

For each test case, print in 4 lines the sum, difference, product and quotient of the two rational numbers, respectively. The format of each line is `number1 operator number2 = result`. Notice that all the rational numbers must be in their simplest form `k a/b`, where `k` is the integer part, and `a/b` is the simplest fraction part. If the number is negative, it must be included in a pair of parentheses. If the denominator in the division is zero, output `Inf` as the result. It is guaranteed that all the output integers are in the range of **long int**.

### Sample Input 1:

```in
2/3 -4/2
```

### Sample Output 1:

```out
2/3 + (-2) = (-1 1/3)
2/3 - (-2) = 2 2/3
2/3 * (-2) = (-1 1/3)
2/3 / (-2) = (-1/3)
```

### Sample Input 2:

```in
5/3 0/6
```

### Sample Output 2:

```out
1 2/3 + 0 = 1 2/3
1 2/3 - 0 = 1 2/3
1 2/3 * 0 = 0
1 2/3 / 0 = Inf
```

### Idea



### AC code

```cpp
```


*2023-01-01 周日*