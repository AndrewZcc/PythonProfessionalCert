# 2.1 搜索算法(DFS/BFS)

### 一、深度优先搜索 DFS

**简介**：
深度优先搜索算法，又称DFS(Depth First Search)。DFS算法是一种搜索算法，而 **搜索算法实质上是一种枚举**，即借助计算机的高性能来有目的地枚举一个问题的部分情况或这个问题的所有情况，进而求出问题的解的一种方法。

根据深搜算法的名字，我们很容易知道DFS是按照深度优先的顺序对所有的状态进行搜索的。
DFS算法是递归算法的一种。搜索时沿着树的深度 遍历树的节点，并尽可能深地搜索树的分支(到叶子节点为止)。当节点v的所有边都被访问过时，搜索将回溯到发现节点v的那条边的起始节点。搜索过程一直进行到已发现从源节点可达的所有节点全部被访问为止。

**注意**：使用 深搜本身并不难，而真正的难点 关键在于：剪枝！

参考链接：https://www.cnblogs.com/cyanigence-oi/p/11754514.html

#### 算法实现

```cpp
void DFS(type n){                       //可以描述阶段的状态
    if(符合条件) {cout<<答案;return;}   //出口
    if(可以剪枝) return;                //剪枝
    for (i:1~p){                       //选择该阶段的所有决策
        选择可行决策;                   //剪枝的一种
        标记已访问该点;
        DFS(n+1);                       //进入下一阶段
        (还原访问现场;)  // 下阶段遍历结束时，回溯到前一阶段，同时要还原现场
    }
}
```

五大类 剪枝 方法：

1. 顺序性 剪枝：如果对搜索顺序无要求，优先搜索分支较少的阶段，此时能减少搜索的规模。
2. 重复性 剪枝：在搜索的时候如果有多种方式可以到达一个状态，那么我们只需要搜索一个分支就可以了。
3. 可行性 剪枝：对搜索正确性的一个保证，当分支在递归边界的时候回溯。
4. 最优性 剪枝：在搜索过程中，如果当前阶段的代价已经超过我们已知的最小代价，那么此时继续搜索下去就失去了意义。
5. 记忆化 剪枝：记录搜索状态的结果，当重复遍历一个状态的时候就可以直接返回这个状态的答案，避免重复的搜索。

#### 典型例题
【黄金矿工】https://leetcode-cn.com/problems/path-with-maximum-gold/

### 二、宽度优先搜索 BFS

**简介：**
 广度优先搜索（也称宽度优先搜索，缩写BFS，以下采用广度来描述）是连通图的一种遍历算法这一算法也是很多重要的图的算法的原型。Dijkstra单源最短路径算法和Prim最小生成树算法都采用了和宽度优先搜索类似的思想。其别名又叫BFS，属于一种盲目搜寻法，目的是系统地展开并检查图中的所有节点，以找寻结果。换句话说，它并不考虑结果的可能位置，彻底地搜索整张图，直到找到结果为止。**基本过程，BFS是从根节点开始，沿着树(图)的宽度遍历树(图)的节点。**如果所有节点均被访问，则算法中止。一般用队列数据结构来辅助实现BFS算法。

https://www.jianshu.com/p/bff70b786bb6

#### 典型例题

https://leetcode-cn.com/problems/number-of-islands/

```python
class Solution(object):
    def infect(self, grid, i, j):
        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]) or grid[i][j] != '1':
            return
        grid[i][j] = '2'
        # 递归遍历它的所有相邻节点
        self.infect(grid, i+1, j)
        self.infect(grid, i-1, j)
        self.infect(grid, i, j+1)
        self.infect(grid, i, j-1)

    def numIslands(self, grid):
        row = len(grid)
        if row == 0:
            return 0
        col = len(grid[0])

        ans = 0
        for i in range(row):
            for j in range(col):
                if grid[i][j] == '1':
                    self.infect(grid, i, j)
                    ans += 1
        return ans
```