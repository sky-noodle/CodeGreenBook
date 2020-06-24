# CodeGreenBook

#Leetcode

[1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

 

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]



```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        		if (nums == null || nums.length < 2)
			return null;
		HashMap<Integer, Integer> res = new HashMap<Integer, Integer>();
		int[] a = new int[2];
		for (int i = 0; i < nums.length; i++) {
			if (res.containsKey(target - nums[i])) {
			a[1] = i;
			// a[0]=i;
			// a[1]=res.get(target-nums[i]);
			break;
		}
		res.put(nums[i], i);
	}
	return a;
}
}
```





