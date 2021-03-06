# DP-1

## 1. Matrix DP

#### [64. 最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

```
[
  [1,3,1],
  [1,5,1],
  [4,2,1] 
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```

```
class Solution {
    public int minPathSum(int[][] grid) {
   //若为空直接返回
        if (grid == null) {
            return 0;
        }
        int m = grid.length;
        int n = grid[0].length;
        int[][]dp = new int[m][n];
        //init
        dp[0][0] = grid[0][0];
        for(int i=1;i<m;i++){
            dp[i][0] = dp[i-1][0]+grid[i][0];
        }
        for(int i=1;i<n;i++){
            dp[0][i]=dp[0][i-1]+grid[0][i];
        }
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j]=Math.min(dp[i-1][j],dp[i][j-1])+grid[i][j];
            }
        }
        return dp[m-1][n-1];
    }
}
```

#### [62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)

输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右

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

#### [63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)

```
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
```

```
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0 || obstacleGrid[0].length == 0) {
            return 0;
        }

        int n = obstacleGrid.length;
        int m = obstacleGrid[0].length;
        int[][] paths = new int[n][m];

        for (int i = 0; i < n; i++) {
            if (obstacleGrid[i][0] != 1) {
                paths[i][0] = 1;
            } else {
                break;
            }
        }

        for (int i = 0; i < m; i++) {
            if (obstacleGrid[0][i] != 1) {
                paths[0][i] = 1;
            } else {
                break;
            }
        }
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                if (obstacleGrid[i][j] != 1) {
                    paths[i][j] = paths[i - 1][j] + paths[i][j - 1];
                } else {
                    paths[i][j] = 0;
                }
            }
        }
        return paths[n - 1][m - 1];
    }
}
```

## 2.Sequences DP

#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

```
int climbStairs(int n){
        int f1 = 1;
        int f2 = 2;
        int res =0;
        if(n<=0)
          return 0;
        if(n<3)
        	return n;
        for(int i=3;i<=n;i++) {
        	res = f1+f2;
        	f1=f2;
        	f2=res;
        }
        return res;
}
```

#### [55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

```
输入: [2,3,1,1,4]
输出: true
```

```
class Solution {
    public boolean canJump(int[] nums) {
        if(nums==null||nums.length==0){
            return false;
        }
        int max = 0;
        for(int i=0;i<nums.length;i++){
            if(i<=max){
                max = Math.max(max,i+nums[i]);
            }
            if(max>=nums.length-1){
                return true;
            }
        }
        return false;
    }
}
```

```
    dp[i]表示从起点出发能不能走到位置；
    dp[i]= dp[j] and nums[j]+j>=i;
    
    
    public boolean canJump(int[] nums) {
        if(nums==null||nums.length==0){
            return false;
        }
        boolean[] dp = new boolean[nums.length];
        dp[0]= true;
        for(int i=1;i<nums.length;i++){
            for(int j=0;j<i;j++) {
                if (dp[j] && (j + nums[j] >= i)) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[nums.length-1];
    }
```



#### [45. 跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)

```
最小跳跃次数
输入: [2,3,1,1,4]
输出: 2
```

```
class Solution {
    public int jump(int[] nums) {
        int len = nums.length;
        int end = 0;
        int step = 0;
        int max = 0;
        for(int i=0;i<len;i++){
            max = Math.max(max,nums[i]+i);
            if(i == end){
                end = max;
                step=step+1;
            }
        }
        return step;
    }
}
```

#### [132. 分割回文串 II](https://leetcode-cn.com/problems/palindrome-partitioning-ii/)

```
输入: "aab"
输出: 1
```

```
class Solution {
    public int minCut(String s) {
        if(s==null||s.length()==0){
            return 0;
        }
        int [] cut = new int[s.length()+1];
        boolean[][] isSub =isSubStr(s);
        cut[0]=0;
        for(int i=1;i<=s.length();i++){
            cut[i]=Integer.MAX_VALUE;
            for(int j=0;j<i;j++){
                if(isSub[j][i-1]){
                    cut[i]=Math.min(cut[i],cut[j]+1);
                }
            }
        }
        return cut[s.length()]-1;
    }
    private boolean[][] isSubStr(String s){
        boolean[][] isSub = new boolean[s.length()][s.length()];
        for(int i=0;i<s.length();i++){
            isSub[i][i]=true;
        }
        for(int i=0;i<s.length()-1;i++){
            isSub[i][i+1] = (s.charAt(i)==s.charAt(i+1));
        }
        for(int i=2;i<s.length();i++){
            for(int j=0;j+i<s.length();j++){
                isSub[j][j+i] = (isSub[j+1][i+j-1])&&(s.charAt(j)==s.charAt(i+j));
            }
        }
        return isSub;
    }
}
```

#### [139. 单词拆分](https://leetcode-cn.com/problems/word-break/)

```
s = "leetcode", wordDict = ["leet", "code"]
```

```
class Solution {
    private int maxLen(List<String> wordDict){
        int max = 0;
        for(String s : wordDict){
            max = Math.max(max,s.length());
        }
        return max;
    }
    public boolean wordBreak(String s, List<String> wordDict) {
        int max = maxLen(wordDict);
        int len = s.length();
        boolean[] dp = new boolean[len+1];
        dp[0] = true;
        for(int i=1;i<=len;i++){
            dp[i]=false;
            for(int j=1;j<=max&&j<=i;j++){
                if(!dp[i-j]){
                    continue;
                }
                String word = s.substring(i-j,i);
                if(wordDict.contains(word)){
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp[len];
        }
}
```

#### [300. 最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
```

```
//dp[i]=MAX{dp[j]+1,nums[j]<nums[i]}
 
class Solution {
    public int lengthOfLIS(int[] nums) {
        int len = nums.length;
        int max = 0;
        int[] dp = new int[len];
        for(int i=0;i<len;i++){
            dp[i]=1;
            for(int j=0;j<i;j++){
                if(nums[j]<nums[i]){
                    dp[i] = Math.max(dp[i],dp[j]+1);
                }
            }
            max = Math.max(max,dp[i]);
        }
    return max;
    }
}
```

## 3.Two Sequences DP

```
dp[i][j]:代表数组1的前i匹配数组2的前j；
function：研究第i和第j匹配关系；
init：dp[i][0]和dp[0][i]
```





#### [1143. 最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)

```
输入：text1 = "abcde", text2 = "ace" 
输出：3  
```

```
dp[i][j] 表示text1以i结尾，text2以j结尾的最长公共子序列长度；
dp[i][j]=dp[i-1][j-1]+1 //text[i]==text[j]
				=max{dp[i-1][j],dp[i][j-1]} //text[i]!=text[j]
下标问题：由于下标从0开始计数，因此dp数组的dp[i][0]和dp[0][j]初始化为0；
比较text[i]与text[j]时，去下标i-1，j-1
最终结果为dp[iLen][jLen];
```

```
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int iLen = text1.length();
        int jLen = text2.length();
        int[][] dp = new int[iLen+1][jLen+1];
        for(int i=1;i<=iLen;i++){
            for(int j=1;j<=jLen;j++){
                if(text1.charAt(i-1)==text2.charAt(j-1)){
                    dp[i][j]=dp[i-1][j-1]+1;
                }else {
                    dp[i][j]=Math.max(dp[i][j-1],dp[i-1][j]);
                }
            }
        }
        return dp[iLen][jLen];
    }
}
```

### [79. 最长公共子串](https://www.lintcode.com/problem/longest-common-substring/description)

```
状态转移方程：dp[i][j]= dp[i-1][j-1]+1 //A[i]==B[j]
									 = 0 //A[i]!=B[j]
```

```
    public int longestCommonSubstring(String A, String B) {
        if(A==null || B==null){
            return 0;
        }
        // write your code here
                int ALen = A.length();
        int BLen = B.length();
        int res=0;
        int[][] dp = new int[ALen+1][BLen+1];
        for(int i =1;i<=ALen;i++){
            for(int j=1;j<=BLen;j++){
                if(A.charAt(i-1)==B.charAt(j-1)){
                    dp[i][j]=dp[i-1][j-1]+1;
                }else {
                    dp[i][j]=0;
                }
                res = Math.max(res,dp[i][j]);
            }
        }
        return res;
    }
```

#### [72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)

```
dp[i][j] str1 的前i个字符变换成str的前j个字符的编辑距离；
dp[i][j] = min{dp[i][j-1]+1,dp[i-1][j-1],dp[i][j]}  str1[i]==str[j]
				= min{dp[i][j-1]+1，dp[i-1][j]+1,dp[i-1][j-1]+1}
dp[i][j-1]+1 //  插入一个字符
d[i-1][j]+1 // 删除一个字符

```

#### [115. 不同的子序列](https://leetcode-cn.com/problems/distinct-subsequences/)

```
dp[i][j] 表示str1前字符中选择str2的前j字符有多少种方案；
dp[i][j] = dp[i-1][j-1]+dp[i-1][j]    str[i]==str[j]
				=dp[i-1][j] str[i]!=str[j]
str2[j] 是匹配的字符，所以不能扔，但是str1[i]可以扔掉计算总共方案个数
```



#### [516. 最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)

```
可以理解为求ｓ和ｓ的逆序的最长公共子序列
dp[i][j] 表示i 字符到 j 字符的最长共子序列
dp[i][j]= dp[i+1][j-1] +2  // s[i]==s[j]
max{dp[i+1][j] ,dp[i][j-1]}
遍历技巧，i 从后往前遍历，j 从i+1 位置往后遍历，保证遍历的是之前遍历过的dp存储结果；
```

```
class Solution {
    public int longestPalindromeSubseq(String s) {
        if(s==null || s.length()==0){
            return 0;
        }
        int len = s.length();
        int[][] dp = new int[len][len];
        int res =1;
        for(int i=len-1;i>=0;i--){
            dp[i][i]=1;
            for(int j=i+1;j<len;j++){
                if(s.charAt(i)==s.charAt(j)){
                    dp[i][j]=dp[i+1][j-1]+2;
                }else{
                    dp[i][j]=Math.max(dp[i+1][j],dp[i][j-1]);
                }
                res = Math.max(dp[i][j],res);
            }
        }
        return res;
    }
}
```



