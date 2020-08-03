# CodeGreenBook

### Leetcode

#### [62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。

1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/unique-paths
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

```
state：dp[x][y] 从起点到x，y路径数
function：（考虑最后一步）
dp[x][y]=dp[x-1][y]+dp[x][y-1]
init:
dp[0][0]=1
dp[0][i]=1
dp[i][0]=1
answer:dp[n-1][m-1]
```

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int uniquePaths(int m, int n) {
     int[][] dp=new int[m][n];
        dp[0][0] = 1;
        for (int i = 0; i < m; i ++){
            for (int j = 0; j < n; j ++){
                if (i == 0 || j == 0){
                    dp[i][j] = 1;
                }
                else{
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
        }
        return dp[m - 1][n - 1];
    }
}

```







