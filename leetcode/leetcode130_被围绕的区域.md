# CodeGreenBook

### Leetcode

[130.被围绕的区域](https://leetcode-cn.com/problems/surrounded-regions/)

给定一个二维的矩阵，包含 'X' 和 'O'（字母 O）。

找到所有被 'X' 围绕的区域，并将这些区域里所有的 'O' 用 'X' 填充。

示例:

X X X X
X O O X
X X O X
X O X X
运行你的函数后，矩阵变为：

X X X X
X X X X
X X X X
X O X X

解释:

被围绕的区间不会存在于边界上，换句话说，任何边界上的 'O' 都不会被填充为 'X'。 任何不在边界上，或不与边界上的 'O' 相连的 'O' 最终都会被填充为 'X'。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/surrounded-regions
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

二维dfs，在二维矩阵中需要从上下左右四个方向搜索；

本题的切入点在‘D'站位思路：

如果O区域和边界连接，则不可能被X包围；

剩下的O则为需要置X的点；

从边界运用dfs，如果为O则置为D；

dfs结束后遍历二维矩阵，D置为O，O置为X；

### 算法设计技巧：

1.从四条边界进行dfs；

2.dfs从上下左右四个方向，把遇到的O置为D；

### 注意点：



代码：

```

class Solution {
    public void solve(char[][] board) {
        if(board==null || board.length==0)
            return;
        int row = board.length;
        int col = board[0].length;
        for(int i=0;i<row;i++){
            dfs(board,i,0);
            dfs(board,i,col-1);
        }
        for(int i=0;i<col;i++){
            dfs(board,0,i);
            dfs(board,row-1,i);
        }
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(board[i][j]=='D'){
                    board[i][j]='O';
                }else if(board[i][j]=='O'){
                    board[i][j]='X';
                }
            }
        }
        return;

    }
    void dfs(char[][] board,int x,int y){
        if(x<0||x>board.length-1||y<0||y>board[0].length-1
        ||board[x][y]!='O') return;
        board[x][y]='D';
        dfs(board,x-1,y);
        dfs(board,x+1,y);
        dfs(board,x,y-1);
        dfs(board,x,y+1);
    }
}
```







