## [题目详情 - 1022 Digital Library (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/problems/994805480801550336)

[1499. 数字图书馆 - AcWing题库](https://www.acwing.com/problem/content/1501/)

#模拟 #set #sstream #排序

A Digital[^1] Library contains millions of books, stored according to their titles, authors, key words of their abstracts, publishers[^2], and published years. Each book is assigned an unique[^3] 7-digit number as its ID. Given any query[^4] from a reader, you are supposed to output the resulting[^5] books, sorted in increasing order of their ID's.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer $N (≤10^4)$ which is the total number of books. Then $N$ blocks follow, each contains the information of a book in 6 lines:

- Line #1: the 7-digit ID number;
- Line #2: the book title -- a string of no more than 80 characters;
- Line #3: the author -- a string of no more than 80 characters;
- Line #4: the key words -- each word is a string of no more than 10 characters without any white space, and the keywords are separated by exactly one space;
- Line #5: the publisher -- a string of no more than 80 characters;
- Line #6: the published year -- a 4-digit number which is in the range [1000, 3000].

It is assumed that each book belongs to one author only, and contains no more than 5 key words; there are no more than 1000 distinct[^6] key words in total; and there are no more than 1000 distinct publishers.

After the book information, there is a line containing a positive integer $M (≤1000)$ which is the number of user's search queries. Then $M$ lines follow, each in one of the formats shown below:

- 1: a book title
- 2: name of an author
- 3: a key word
- 4: name of a publisher
- 5: a 4-digit number representing the year

### Output Specification:

For each query, first print the original query in a line, then output the resulting book ID's in increasing order, each occupying a line. If no book is found, print `Not Found` instead.

### Sample Input:

```in
3
1111111
The Testing Book
Yue Chen
test code debug sort keywords
ZUCS Print
2011
3333333
Another Testing Book
Yue Chen
test code sort keywords
ZUCS Print2
2012
2222222
The Testing Book
CYLL
keywords debug book
ZUCS Print2
2011
6
1: The Testing Book
2: Yue Chen
3: keywords
4: ZUCS Print
5: 2011
3: blablabla
```

### Sample Output:

```out
1: The Testing Book
1111111
2222222
2: Yue Chen
1111111
3333333
3: keywords
1111111
2222222
3333333
4: ZUCS Print
1111111
5: 2011
1111111
2222222
3: blablabla
Not Found
```

### Idea

1. `keyword` 不确定是几个字符,使用`sstream` 进行输入,使用 `set` 进行查询操作(比 `map` 方便)
2.  `id, name, author` 使用 `string` 存储
3. `publisher, year` 使用 `string` 进行存储

### AC code

```cpp
#include <iostream>
#include <set>
#include <vector>
#include <sstream>
#include <algorithm>

using namespace std;

struct Book{
    string id, name, author;
    set<string> keywords;
    string publisher, year;
};

int main(void){

    int n, m;
    vector<Book> books;

    cin >> n;
    while(n--){
        string id, name, author;
        cin >> id;
        getchar();
        getline(cin, name);
        getline(cin, author);

        string line;
        getline(cin, line);
        stringstream ssin(line);
        string keyword;
        set<string> keywords;
        while(ssin >> keyword) keywords.insert(keyword);

        string publisher, year;
        getline(cin, publisher);
        cin >> year;

        books.push_back({id, name, author, keywords, publisher, year});
    }

    cin >> m;
    getchar();
    string line;
    while(m--){
        getline(cin, line);
        cout << line << endl;

        string info = line.substr(3);
        char t = line[0];
        vector<string> res;

        if(t == '1'){
            for(auto& book : books){
                if(book.name == info) res.push_back(book.id);
            }
        }
        else if(t == '2'){
            for(auto& book : books){
                if(book.author == info) res.push_back(book.id);
            }
        }
        else if(t == '3'){
            for(auto& book : books){
                if(book.keywords.count(info)) res.push_back(book.id);
            }
        }
        else if(t == '4'){
            for(auto& book : books){
                if(book.publisher == info) res.push_back(book.id);
            }
        }
        else{
            for(auto& book : books){
                if(book.year == info) res.push_back(book.id);
            }
        }

        if(res.empty()) puts("Not Found");
        else{
            sort(res.begin(), res.end());
            for(auto item : res) cout << item << endl;
        }
    }

    return 0;
}
```


*2022-07-25 周一*

[^1]: digital $adj.$ 数字的
[^2]: publisher $n.$ 出版商
[^3]: unique $adj.$ 独一无二的
[^4]: query $n.$ 询问
[^5]: resulting $adj.$ 作为结果的
[^6]: distinct $adj.$ 不同的