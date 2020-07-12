# CodeGreenBook

### Leetcode

#### [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)



假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

示例 1:

输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
示例 2:

输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/search-in-rotated-sorted-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

1.mid元素先跟left比，

如果mid比left大，则mid在原始递增数组；

否则在右侧旋转数组；

2.mid在原始数组，如果left<target且mid>target，说明target在left与mid之间=>right=mid；

否则在mid右侧=>left=mid;

3.mid在旋转数组，如果target>mid且right>target，说明target在mid与right、之间=>left=mid;

否则在mid左侧=>right=mid;

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int search(int[] nums, int target) {
        if(nums==null || nums.length==0)
        return -1;
        int left =0;
        int right = nums.length-1;
        int mid = 0;
        while(left+1<right){
            mid = (left+right)/2;
            if(nums[mid]==target)
                return mid;
            if(nums[mid]>nums[left]){
                if(nums[left]<=target && nums[mid]>=target){
                    right = mid;
                }else{
                    left = mid;
                }
            }else{
                if(target>=nums[mid] && target<=nums[right]){
                    left = mid;

                }else{
                    right=mid;
                }
            }
        }
        if(nums[left] == target){
            return left;
        }
        if(nums[right] == target)
        return right;
        return -1;


    }
}

```







