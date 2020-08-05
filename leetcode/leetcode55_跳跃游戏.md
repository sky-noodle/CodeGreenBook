# CodeGreenBook

### Leetcode

#### [55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

示例 1:

输入: [2,3,1,1,4]
输出: true
解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/jump-game
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。 

### 思路：

```
state: f[i]表示能否跳到位置
function: f[i] = or（f[j],i>j&&j能跳到i)//
intialize: f[0]=true
answer: f[n-1]
```

### 算法设计技巧：

如果j位置能跳到i，则break即可，减少计算；

### 注意点：



代码：

```
class Solution {
    public boolean canJump(int[] nums) {
        if(nums==null||nums.length==0){
            return false;
        }
        int len = nums.length;
        boolean[] dp = new boolean[len];
        dp[0]=true;
        for(int i=1;i<len;i++){
            for(int j=0;j<i;j++){
                if(dp[j]&&nums[j]+j>=i){
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp[len-1];

    }
}
```



```
Version2：Greedy
public boolean conJump(int[] A){
	if(A==null || A.length==0){
		return false;
	}
	int forthest = A[0];
	for(int i=1;i<A.length;i++){
		if(i<=forthest&&A[i]+i>=forthest){
			forthest=A[i]+i;
      }
	}
	return forthest>=A.length-1;
}
```







