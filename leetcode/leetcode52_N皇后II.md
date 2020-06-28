# CodeGreenBook

### Leetcode

[52.N皇后II](https://leetcode-cn.com/problems/n-queens-ii/)

*n* 皇后问题研究的是如何将 *n* 个皇后放置在 *n*×*n* 的棋盘上，并且使皇后彼此之间不能相互攻击。

输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]

提示：

皇后，是国际象棋中的棋子，意味着国王的妻子。皇后只做一件事，那就是“吃子”。当她遇见可以吃的棋子时，就迅速冲上去吃掉棋子。当然，她横、竖、斜都可走一或七步，可进可退。（引用自 百度百科 - 皇后 ）

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/n-queens-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：



### 算法设计技巧：

1.设计loc数组，{3,1,4,2}代表放置位置（1，3），（2，1），（3，4），（4，2）；



### 注意点：



代码：

```
class Solution {
    int res;
    public int totalNQueens(int n) {
        res = 0;
        if(n<=0) return res;
        int[] loc = new int[n];
        dfs(n, loc,0);
        return res;
    }
    void dfs(int n,int[] loc,int cur){
        if(cur==n){
            res++;
            return;
        }
        for(int i=0;i<n;i++){
            loc[cur]=i;
            if(isValid(loc,cur)){
                dfs(n,loc,cur+1);
            }
        }
    }
    boolean isValid(int[] loc,int cur){
        for(int i=0;i<cur;i++){
            if(loc[i]==loc[cur] || Math.abs(loc[i]-loc[cur])==(cur-i))
                return false;
        }
        return true;
    }
    
}

```







