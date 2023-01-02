## [题目详情 - 1123 Is It a Complete AVL Tree (pintia.cn)](https://pintia.cn/problem-sets/994805342720868352/exam/problems/994805351302414336)

[1616. 判断完全 AVL 树 - AcWing题库](https://www.acwing.com/problem/content/1618/)

An AVL tree is a self-balancing binary search tree. In an AVL tree, the heights of the two child subtrees of any node differ by at most one; if at any time they differ by more than one, rebalancing is done to restore this property. Figures 1-4 illustrate the rotation rules.

|![[Is It a Complete AVL Tree 配图_1.jpg]]|![[Is It a Complete AVL Tree 配图_2.jpg]]|
|---|---|
|![[Is It a Complete AVL Tree 配图_3.jpg]]|![[Is It a Complete AVL Tree 配图_4.jpg]]|

Now given a sequence of insertions, you are supposed to output the level-order traversal sequence of the resulting AVL tree, and to tell if it is a complete binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer $N ( \leq  20)$. Then N distinct integer keys are given in the next line. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, insert the keys one by one into an initially empty AVL tree. Then first print in a line the level-order traversal sequence of the resulting AVL tree. All the numbers in a line must be separated by a space, and there must be no extra space at the end of the line. Then in the next line, print `YES` if the tree is complete, or `NO` if not.

### Sample Input 1:

```in
5
88 70 61 63 65
```

### Sample Output 1:

```out
70 63 88 61 65
YES
```

### Sample Input 2:

```in
8
88 70 61 96 120 90 65 68
```

### Sample Output 2:

```out
88 65 96 61 70 90 120 68
NO
```

### Idea



### AC code

```cpp
```


*2022-12-31 周六*