## [题目详情 - 1015 Reversible Primes (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805495863296000)

[1492. 可逆质数 - AcWing题库](https://www.acwing.com/problem/content/1494/)

#进位制 #质数

A **reversible prime** in any number system is a prime whose "reverse" in that number system is also a prime. For example in the decimal system 73 is a reversible prime because its reverse 37 is also a prime.

Now given any two positive integers $N (<10^5)$ and $D (1<D≤10)$, you are supposed to tell if N is a reversible prime with radix $D$.

### Input Specification:

The input file consists of several test cases. Each case occupies a line which contains two integers $N$ and $D$. The input is finished by a negative $N$.

### Output Specification:

For each test case, print in one line `Yes` if $N$ is a reversible prime with radix $D$, or `No` if not.

### Sample Input:

```in
73 10
23 2
23 10
-2
```

### Sample Output:

```out
Yes
Yes
No
```

### Idea

1. 判断 $N$ 是否是质数
2. 将 $N$ 转化为在 $D$ 进制下的数
3. 将该数进行翻转
4. 将翻转后的数转换为十进制的数
5. 判断该数是否是质数


$D$ 进制想要转化成十进制每次要乘 $D$(秦九韶算法)

经过分析,可以发现可以在使用秦九韶算法的过程中完成 2. 3. 4. 步骤

### AC code

```cpp
#include <iostream>

using namespace std;

bool is_prime(int n){
    if(n < 2) return false;
    for(int i = 2; i <= n / i; i++){
        if(n % i == 0) return false;
    }
    return true;
}

bool check(int n, int m){
    if(!is_prime(n)) return false;

    int ans = 0;
    while(n){
        ans = ans * m + n % m;
        // n % m 的结果就是n在d进制下的最后一位
        // ans * m 就是十进制的数
        n /= m;
    }

    return is_prime(ans);
}

int main(void){

    int n, m;

    while(cin >> n >> m, n >= 1){
        if(check(n, m)) puts("Yes");
        else puts("No");
    }

    return 0;
}
```


*2022-07-21 周四*