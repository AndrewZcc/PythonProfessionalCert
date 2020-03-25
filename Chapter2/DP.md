# 2.8 动态规划

思想：动态规划与分治法类似，都是 **把大问题拆分成小问题**，通过寻找大问题与小问题的递推关系，解决一个个小问题，最终达到解决原问题的效果。但不同的是，分治法在子问题和子子问题等上被重复计算了很多次，而 **动态规划则具有记忆性**，通过填写表把所有已经解决的子问题答案纪录下来，在新问题里需要用到的子问题可以直接提取，**避免重复计算，从而节约了时间**，所以在 <u>问题满足最优性原理之后，用动态规划解决问题的核心就在于填表，表填写完毕，最优解也就找到</u>。

#### 两类求解方法

* 一、带备忘的自顶向下法
* 二、自底向上法

#### 例题
##### 1、钢条切割问题
方法一：自大到小求解 + 备忘
**递归求解表达式：r[n] = max(p[i] + r[n-i]) for i in range(1,n)**

记录重复子问题的解：r[n]

方法二：自小到大 逆向求解
```python
res[0] = 0
for j in range(1, n):
	q = float('-inf')
	for i in range(i, j)
		q = max(q, price[i] + res[j-i])
	res[j] = q
return res[n]
```
##### 2、0-1 背包问题
题目：有N个物品和一个容量为W的背包，给出每个物品的重量和价值，求能装入背包中所有物品的最大总价值。

递归表达式（状态转移方程）
```
if (w[i] <= j)
	m[i][j] = max(m[i-1][j], m[i-1][j-w[i]]+v[i]);
else
	m[i][j] = m[i-1][j];
```

##### 3、最小路径和
[最小路径和] https://leetcode-cn.com/problems/minimum-path-sum/

状态转移方程：`dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`

```python
class Solution:
    def minPathSum(self, grid):
        M = len(grid)
        if M <= 0:
            return 0
        N = len(grid[0])
        dp = [[0]*N for i in range(0, M)]
        dp[0][0] = grid[0][0]
        for i in range(0, M):
            for j in range(0, N):
                if i == 0 and j == 0:
                    continue
                elif i == 0:
                    min_value = dp[i][j-1]
                elif j == 0:
                    min_value = dp[i-1][j]
                else:
                    min_value = min(dp[i-1][j], dp[i][j-1])
                dp[i][j] = grid[i][j] + min_value
        return dp[M-1][N-1]
```

