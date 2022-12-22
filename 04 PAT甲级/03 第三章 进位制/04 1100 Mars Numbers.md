## [题目详情 - 1100 Mars Numbers (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805367156883456)

[1590. 火星数字 - AcWing题库](https://www.acwing.com/problem/content/1592/)

#进位制 #sstream

People on Mars count their numbers with base 13:

- Zero on Earth is called "tret" on Mars.
- The numbers 1 to 12 on Earth is called `"jan, feb, mar, apr, may, jun, jly, aug, sep, oct, nov, dec"` on Mars, respectively.
- For the next higher digit, Mars people name the 12 numbers as `"tam, hel, maa, huh, tou, kes, hei, elo, syy, lok, mer, jou"`, respectively.

For examples, the number 29 on Earth is called `"hel mar"` on Mars; and `"elo nov"` on Mars corresponds to $115$ on Earth. In order to help communication between people from these two planets, you are supposed to write a program for mutual translation between Earth and Mars number systems.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer $N (<100)$. Then $N$ lines follow, each contains a number in $[0, 169)$, given either in the form of an Earth number, or that of Mars.

### Output Specification:

For each number, print in a line the corresponding number in the other language.

### Sample Input:

```in
4
29
5
elo nov
tam
```

### Sample Output:

```out
hel mar
may
115
13
```

### Idea

1. 本题输入不确定具体是什么类型,如果读入的是字符串,也不确定字符串中的具体内容,所以使用 `sstream` 进行处理
2. 有题目可知,本题的范围最大到 $168$ ,故输出的字符串就多不会超过 $2$ 个
3. 在使用 `getline` 的时候,需要将上一行的空格给过滤掉

### AC code

```cpp
#include <iostream>
#include <sstream>

using namespace std;

char name[][5] ={
    "tret", "jan", "feb", "mar", "apr", "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec",
    "tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"
};

int get(string word){
    for(int i = 0; i < 25; i++){
        if(name[i] == word){
            if(i < 13) return i;
            else return (i - 12) * 13;
        }
    }
}

int main(void){

    int n;
    cin >> n;
    getchar();

    while(n--){
        string line;
        getline(cin, line);

        stringstream ssin(line);
        if(line[0] <= '9'){// 如果读入的数字
            int v;
            ssin >> v;// 读出数字
            if(v < 13) cout << name[v] << endl;// 输出是个位的情况
            else{
                cout << name[12 + v / 13];
                if(v % 13 == 0) cout << endl;// 对13进行特判
                else cout << ' ' << name[v % 13] << endl;
            }
        }
        else{
            int res = 0;
            string word;
            while(ssin >> word) res += get(word);
            cout << res << endl;
        }
    }

    return 0;
}
```


*2022-07-24 周日*