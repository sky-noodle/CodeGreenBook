# CodeGreenBook

### Leetcode

[79.单词搜索](https://leetcode-cn.com/problems/word-search/)

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

示例:

board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false

提示：

board 和 word 中只包含大写和小写英文字母。
1 <= board.length <= 200
1 <= board[i].length <= 200
1 <= word.length <= 10^3

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/word-search
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

先遍历二维数组，找到单词起点，上下左右dfs；

dfs返回boolean，如果找到匹配的字符则继续下一次搜索，否则跳到上一层，直到最后一个字符匹配成功；

### 算法设计技巧：

1.每个字符只能使用一次，每匹配一个字符，就先将该字符改为“ ”，如果匹配失败返回，将字符改为原来字符；

2.设计dir 表示上下左右；

### 注意点：



代码：

```
class Solution {
    public boolean exist(char[][] board, String word) {
        if(board==null || board.length==0)
            return false;
        int row = board.length;
        int col = board[0].length;
        char c = word.charAt(0);
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(board[i][j]==c){
                    board[i][j]=' ';
                    if(dfs(board,word.substring(1),i,j)) return true;
                    board[i][j]=c;
                }
            }
        }
        return false;
    }
    boolean dfs(char[][] board, String word,int x,int y){
        if(word.length()==0) return true;
        int[][] dir = {{-1,0},{1,0},{0,-1},{0,1}};
        char c = word.charAt(0);
        for(int in =0;in<4;in++){
            int i=x+dir[in][0];
            int j=y+dir[in][1];
            if(i>=0&&i<board.length&&j>=0&&j<board[0].length&&board[i][j]==c){
                board[i][j]=' ';
                if(dfs(board,word.substring(1),i,j)) return true;
                board[i][j]=c;
            }
        }
        return false;
    }
}

```







