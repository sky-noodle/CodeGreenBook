# CodeGreenBook

### Leetcode



[79.子集II][https://leetcode-cn.com/problems/subsets-ii/ ]

给定一个可能包含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:

输入: [1,2,2]
输出:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subsets-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

思路与 78.子集一致，区别点在于输入数组中存在重复数字；

如果上题解法不修改，则会导致引入重复子集问题；

因此在删除元素后，取新加入元素时，需要与前一元素比较，直到非相同元素；

加入下面一句：

```
while(i<nums.length-1&&nums[i]==nums[i+1]) i++;
```

### 算法设计技巧：

1.while目地为判断当前元素于删除元素是否相同，如果不相同回溯，否则跳过；

### 注意点：

1.i<nums.length-1 小心i溢出；

2.建议nums[i]==nums[i+1] 条件放入while循环中，

如果写成 while(i<nums.length-1) if(nums[i]==nums[i+1]) i++,在不相同时则导致死循环，记得加break；



代码：

```
import java.util.*;
class Solution {
				public List<List<Integer>> subsetsWithDup(int[] nums) {
				List<List<Integer>> res = new ArrayList<List<Integer>>();
        ArrayList<Integer> tmp = new ArrayList();
        int[] arr = Arrays.copyOf(nums,nums.length);
        Arrays.sort(arr);
        res.add(tmp);
        dfs(arr,res,tmp,0);
        return res;
    }
    public void dfs(int[] nums,List<List<Integer>> res,ArrayList<Integer>  tmp,int pos){
        for(int i=pos;i<nums.length;i++){
            tmp.add(nums[i]);
            res.add(new ArrayList<Integer>(tmp));
            dfs(nums,res,tmp,i+1);
            tmp.remove(tmp.size()-1);
            while(i<nums.length-1&&nums[i]==nums[i+1]) i++;
        }
    }
}
```







