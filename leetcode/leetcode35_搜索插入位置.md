# CodeGreenBook

### Leetcode

#### [35. 搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

示例 1:

输入: [1,3,5,6], 5
输出: 2
示例 2:

输入: [1,3,5,6], 2
输出: 1

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/search-insert-position
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

转化为，寻找数组中第一个大于等于targe的数的下标 ；

//或者最后一个小于target的位置加1；

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int searchInsert(int[] nums, int target) {
        int res =0;
        if(nums==null || nums.length==0)
            return res;

        int len = nums.length;
        int left=0;
        int right=len-1;
        int mid=0;
        while (left+1<right){
            mid = left+(right-left)/2;
            if(nums[mid]==target)
                return mid;
            else if(nums[mid]>target){
                right=mid;
            }else{
                left=mid;
            }
        }
        if(nums[left]>=target){
            res=left;
        }
        else if(nums[right]>=target){
            res=right;
        }else{
            return len;
        }
        return res;
    }
}

```







