## [题目详情 - 1071 Speech Patterns (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805398257647616)

[1557. 说话方式 - AcWing题库](https://www.acwing.com/problem/content/1559/)

#双指针 #hash #字符串

People often have a preference among synonyms of the same word. For example, some may prefer "the police", while others may prefer "the cops". Analyzing such patterns can help to narrow down a speaker's identity, which is useful when validating, for example, whether it's still the same person behind an online avatar.

Now given a paragraph of text sampled from someone's speech, can you find the person's most commonly used word?

### Input Specification:

Each input file contains one test case. For each case, there is one line of text no more than 1048576 characters in length, terminated by a carriage return `\n`. The input contains at least one alphanumerical character, i.e., one character from the set [`0-9 A-Z a-z`].

### Output Specification:

For each test case, print in one line the most commonly occurring word in the input text, followed by a space and the number of times it has occurred in the input. If there are more than one such words, print the lexicographically smallest one. The word should be printed in all lower case. Here a "word" is defined as a continuous sequence of alphanumerical characters separated by non-alphanumerical characters or the line beginning/end.

Note that words are case **insensitive**.

### Sample Input:

```in
Can1: "Can a can can a can?  It can!"
```

### Sample Output:

```out
can 5
```

### Idea

1. 先将整个字符串读入
2. 然后使用双针算法将每个单词抠出来,并存储到hash表中
3. 遍历hash表,得出答案

### AC code

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

bool check(char a){
    if(a >= '0' && a <= '9') return true;
    if(a >= 'a' && a <= 'z') return true;
    if(a >= 'A' && a <= 'Z') return true;
    return false;
}

int main(void){

    string str;
    getline(cin, str);

    unordered_map<string, int> hash;
    for(int i = 0; i < str.size(); i++){
        if(check(str[i])){
            string word;
            int j = i;
            while(j < str.size() && check(str[j])) word += towlower(str[j++]);
            hash[word]++;
            i = j;
        }
    }

    string ans;
    int cnt = -1;
    for(auto item : hash){
        if(item.second > cnt || item.second == cnt && item.first < ans){
            ans = item.first;
            cnt = item.second;
        }
    }

    cout << ans << ' ' << cnt << endl;

    return 0;
}
```


*2022-07-18 周一*