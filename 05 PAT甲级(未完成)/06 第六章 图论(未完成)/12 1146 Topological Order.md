## [题目详情 - 1146 Topological Order (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/994805343043829760)

[1639. 拓扑顺序 - AcWing题库](https://www.acwing.com/problem/content/1641/)

This is a problem given in the Graduate Entrance Exam in 2018: Which of the following is NOT a topological order obtained from the given directed graph? Now you are supposed to write a program to test each of the options.

![[Topological Order配图.jpg]]

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers $N ( \leq  1,000)$, the number of vertices in the graph, and $M ( \leq  10,000)$, the number of directed edges. Then M lines follow, each gives the start and the end vertices of an edge. The vertices are numbered from $1$ to $N$. After the graph, there is another positive integer $K ( \leq  100)$. Then K lines of query follow, each gives a permutation of all the vertices. All the numbers in a line are separated by a space.

### Output Specification:

Print in a line all the indices of queries which correspond to "NOT a topological order". The indices start from zero. All the numbers are separated by a space, and there must no extra space at the beginning or the end of the line. It is graranteed that there is at least one answer.

### Sample Input:

```in
6 8
1 2
1 3
5 2
5 4
2 3
2 6
3 4
6 4
6
5 2 3 6 4 1
1 5 2 3 6 4
5 1 2 6 3 4
5 1 2 3 6 4
5 2 1 6 3 4
1 2 3 4 5 6
```

### Sample Output:

```out
0 4 5
```

### Idea



### AC code

```cpp
```


*2023-01-01 周日*