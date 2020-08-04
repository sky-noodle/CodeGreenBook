# CodeGreenBook

## DP

#### 定义：

```

```

#### 2.应用：

```

trick：
三类问题需要朝动归方面想：
1.最值问题（序列、路径的最大值等）
2.是否问题（能否找到一条路径满足X条件） 
3.计数问题（一共多少走法）
同时：
1.不能sort；
2.不能swap；
例如集合问题
```

#### 3.算法设计点：

```
1.状态 state（最核心设计点）
存储小规模问题的结果（dp数组，走到某一步的值）；
2.方程 function
状态之间的联系，怎么通过小的状态，计算大的状态；
3.初始化 intialization
状态起点，最极限的小状态（dp[0][0]直观的状态结果，例如第一步路径）；
4.答案 answer
状态终点，最大的状态（dp[n][n]最终的状态结果，例如最种路径和）；

四类DP：
1.matrix DP （10%）
state：dp[x][y]表示从起点走到坐标x，y
function：考虑走到x，y坐标的前一步
init：带入状态定义中的值（二维dp，需初始化第一行和第一列！）
因为需要x-1和y-1操作，从第二行、第二列开始的内圈进行状态计算会方便很多；
answer：需要的值
[LeetCode] 64. Minimum Path Sum 最小路径和


2.sequence DP （40%）
state: f[i]表示“前i”个位置/数字/字母,(以第i个为)...
function: f[i] = f[j] … j 是i之前的一个位置
intialize: f[0]..
answer: f[n-1].. 
爬楼梯问题

3.two sequence DP （40%）
4.backpack （10%）
```

#### 4.算法模板

```

```

### 5.例题解析


##### 5.1基础题：

 