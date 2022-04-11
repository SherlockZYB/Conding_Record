# 矩阵连乘问题

### 题目描述

已知有  n  个矩阵,第  i  个矩阵的行数为  a \[ i ]  , 列数为  a \[ i + 1 ]  。\
试求把  n  个矩阵乘起来所需要的执行乘法的次数的最小值。\
PS:本题源自助教上算法设计时的原题，不过当时的助教将一个测试点设置为了  n = 2000  从而变成了毒瘤题，有兴趣的同学可以自行思考怎么做...

### 输入描述

第一行是一个正整数  n ( n ≤ 100 )  ，表示矩阵的个数。 第二行有  n + 1  个整数，第  i  个整数表示  a \[ i ]  。

### 输出描述

输出第一行有一个整数，将  n  个矩阵乘起来所要执行的乘法次数的最小值。

### 样例输入

4\
1 2 3 4 5

### 样例输出

38

### 解题方法

```clike
#include<iostream>
#include<string>
#include <algorithm>
#include <climits>

using namespace std;
int p[105];
int m[105][105];
int n;

int LookupChain(int i, int j) {
	if (m[i][j] > 0)
		return m[i][j];
	if (i == j)
		return 0;
	m[i][j] = LookupChain(i, i) + LookupChain(i + 1, j) + p[i - 1] * p[i] * p[j];
	for (int k = i + 1; k < j; k++) {
		int t = LookupChain(i, k) + LookupChain(k + 1, j) + p[i - 1] * p[k] * p[j];
		if (t < m[i][j]) {
			m[i][j] = t;
		}
	}
	return m[i][j];
}


int main() {
	cin >> n;
	for (int i = 0; i < n+1; i++) {
		cin >> p[i];
	}
	cout << LookupChain(1, n) << endl;
	return 0;
}
```

### 做题小结

1. 经典的动态规划方法，动态规划常规步骤如下：
   1. 找出最优解的性质，刻画其结构特征。
   2. 递归地定义最优值。
   3. 以自底向上的方式计算最优值。（如果采用备忘录则是自顶向下）
   4. 根据计算最优值得到的信息构造最优解。
2. 此题的关键在于找出最佳子结构m\[i]\[j]，即矩阵Ai到Aj的最小连乘次数，同时用k来进行划分，求出用k划分出来的所有连乘次数，找出最小值作为m\[i]\[j]；
