## [题目详情 - 1071 Speech Patterns (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805398257647616)

[1557. 说话方式 - AcWing题库](https://www.acwing.com/problem/content/1559/)

#双指针 #hash #字符串 #unordered_map 

People often have a preference[^2] among[^3] synonyms[^4] of the same word. For example, some may prefer "the police", while others may prefer "the cops". Analyzing[^5] such patterns can help to narrow[^6] down[^7] a speaker's identity, which is useful when validating[^8], for example, whether it's still the same person behind an online avatar[^9].

Now given a paragraph[^10] of text sampled[^11] from someone's speech, can you find the person's most commonly[^12] used word?

### Input Specification:

Each input file contains one test case. For each case, there is one line of text no more than 1048576 characters in length, terminated[^13] by a carriage return[^14] `\n`. The input contains at least[^23] one alphanumerical[^15] character, i.e., one character from the set [`0-9 A-Z a-z`].

### Output Specification:

For each test case, print in one line the most commonly occurring[^16] word in the input text, followed by[^17] a space and the number of times it has occurred in the input. If there are more than one such words, print the lexicographically[^18] smallest one. The word should be printed in all lower case[^19]. Here a "word" is defined as a continuous[^20] sequence[^21] of alphanumerical characters separated by non-alphanumerical characters or the line beginning/end.

Note that words are case **insensitive**[^22].

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

bool check(char c){// 检查当前位置是否为单词的一部分
    if(c > '0' && c < '9') return true;
    else if(c > 'a' && c < 'z') return true;
    else if(c > 'A' && c < 'Z') return true;
    return false;
}

int main(void){

    string str;
    getline(cin, str);

    unordered_map<string, int> hash;
    for(int i = 0; i < str.size(); i++){
        if(check(str[i])){// 双指针算法
            string word;
            int j = i;// 从当前位置进行遍历
            while(j < str.size() && check(str[j])) word += towlower(str[j++]);
            hash[word]++;
            i = j;// 跳转位置
        }
    }

    string ans;
    int cnt = -1;
    for(auto item : hash){
        if(item.second > cnt || item.second == cnt && item.first < ans){// &&的优先级比||高
            // 正好可以输出数量最多且字典序最小的常用语句
            ans = item.first;
            cnt = item.second;
        }
    }

    cout << ans << ' ' << cnt << endl;

    return 0;
}
```


*2022-07-18 周一*
			0. pattern $n.$ 方式
[^2]: preference $n.$ 偏爱
[^3]: among $prep.$ 在......当中
[^4]: synonym $n.$ 同义词
[^5]: analyze $vt.$ 对......进行分析
[^6]: narrow $adj.$ 狭窄的
[^7]: narrow down 缩小
[^8]: validate $v.$ 证实, 确认
[^9]: avatar $n.$ 头像
[^10]: paragraph $n.$ 段落
[^11]: sample $n.$ 样本
[^12]: commonly $adv.$ 通常
[^13]: terminate $v.$ 在......结尾
[^14]: carriage return 回车
[^15]: alphanumerical $adj.$ 字母数字混合编制的
[^16]: occur $v.$ 出现
[^17]: followed by 后跟
[^18]: lexicographical $adj.$ 辞典编纂的
[^19]: lower case 小写字母
[^20]: continuous $adj.$ 连续不断的
[^21]: sequence $n.$ 顺序
[^22]: insensitive $adj.$ 不敏感的`
[^23]: at least 至少