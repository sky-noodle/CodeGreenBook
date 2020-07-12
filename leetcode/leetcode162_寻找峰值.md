# CodeGreenBook

### Leetcode

#### [162. 寻找峰值](https://leetcode-cn.com/problems/find-peak-element/)

峰值元素是指其值大于左右相邻值的元素。

给定一个输入数组 nums，其中 nums[i] ≠ nums[i+1]，找到峰值元素并返回其索引。

数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。

你可以假设 nums[-1] = nums[n] = -∞。

示例 1:

输入: nums = [1,2,3,1]
输出: 2
解释: 3 是峰值元素，你的函数应该返回其索引 2。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-peak-element
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 思路：

如果mid与左边元素比，递增关系，则说明mid右侧一定有峰；

如果递减则左边有峰；

如果左边递增右边递减，则说明为峰；

返回any position 模板；

### 算法设计技巧： 



### 注意点：

最终考虑峰值为左右边界情况，即整个数组单调情况；



代码：

```

class Solution {
    public int findPeakElement(int[] nums) {
        if(nums==null || nums.length==0)
        return 0;
        int left = 0;
        int right = nums.length-1;
        int mid=0;
        while(left+1<right){
            mid = (right+left)/2;
            if(nums[mid]>nums[mid-1] && nums[mid]>nums[mid+1]){
                return mid;
            }
            if(nums[mid]>nums[mid-1]){
                left = mid;
            }else{
                right = mid;
            }
        }
        if(left==0 && nums[right]<nums[left])
        return 0;
        if(right==nums.length-1 && nums[right]>nums[left])
        return right;

        return 0;
    }
}
```







