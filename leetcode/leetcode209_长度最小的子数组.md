# CodeGreenBook

### Leetcode

#### [209. 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)



给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的连续子数组，并返回其长度。如果不存在符合条件的连续子数组，返回 0。

 

示例：

输入：s = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的连续子数组。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/minimum-size-subarray-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

左右指针维护滑动窗口；

固定左指针，如果窗口内和<s,右指针移动；

当滑动窗口当窗口内和大于等于s时，计算窗口长度，记录子数组；

左指针移动；

### 算法设计技巧：



### 注意点：

对于无解的情况，在返回最优解时做判断；

代码：

```
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums==null || nums.length==0)
            return 0;
        int l =0;
        int min = Integer.MAX_VALUE;
        int sum = 0;
        for(int r=0;r<nums.length;r++){
            sum+=nums[r];
            while (sum>=s){
                min = Math.min(min,r-l+1);
                sum-=nums[l++];
            }
        }
        return Integer.MAX_VALUE ==min ? 0 : min;
    }
}
```







