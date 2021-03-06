# CodeGreenBook

### Leetcode

#### [45. 跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

示例:

输入: [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/jump-game-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

```
state: f[i]代表我跳到这个位置最少需要几步
function: f[i] = MIN(f[j]+1, j < i && j能够跳到i)
initialize: f[0] = 0;
answer: f[n-1]
```

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int jump(int[] nums) {
        int[] dp = new int[nums.length];
        dp[0]=0;
        for(int i=1;i<nums.length;i++){
            dp[i]=Integer.MAX_VALUE;
            for(int j=0;j<i;j++){
                if(dp[j]!=Integer.MAX_VALUE&&nums[j]+j>=i){
                    dp[i] = dp[j]+1;
                    break;
                }
            }
        }
        return dp[nums.length-1];
    }
}

```







