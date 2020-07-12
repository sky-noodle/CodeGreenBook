# CodeGreenBook

### Leetcode

寻找有序数组特定元素的开始和结束位置；

Description: 
Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm’s runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example, 
Given [5, 7, 7, 8, 8, 10] and target value 8, 
return [3, 4].

### 思路：

分解为两道题，二分找first position和二分找last position；

### 算法设计技巧：



### 注意点：



代码：

```
  public static int[] searchRange(int[] nums,int target){
        int[] res = new int[2];
        if(nums==null || nums.length==0){
            return res;
        }
        res[0] = findFirst(nums, target);
        res[1] = findLast(nums, target);
        return res;
    }
    public static int findFirst(int[] nums, int target){
        int start = 0;
        int end = nums.length-1;
        int mid = 0;
        while (start+1<end){
            mid = start + (end-start)/2;
            if(nums[mid]==target){
                end = mid;
            }else if(nums[mid]<target){
                start=mid;
            }else {
               end=mid;
            }
        }
        if(nums[start]==target){
            return start;
        }
        if(nums[end]==target){
            return end;
        }
        return -1;
    }
    public static int findLast(int[] nums, int target){
        int start = 0;
        int end = nums.length-1;
        int mid = 0;
        while (start+1<end){
            mid = start + (end-start)/2;
            if(nums[mid]==target){
                start = mid;
            }else if(nums[mid]<target){
                start=mid;
            }else {
                end=mid;
            }
        }
        if(nums[end]==target){
            return end;
        }
        if(nums[start]==target){
            return start;
        }
        return -1;
    }
```







