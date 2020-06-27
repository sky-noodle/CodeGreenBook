# CodeGreenBook

## Leetcode



[78.子集][https://leetcode-cn.com/problems/subsets/ ]

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:

输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]

思路：

子集的dfs思路非常直观，每次添加一个元素都是一个新的子集，直到没有元素，回溯到最近一次添加点，直到无元素可添加同时无回溯点；

算法设计技巧：

1.引入int pos 记录当前子集的起点，用于保证不添加重复子集；

2.当前层添加了第i元素，dfs下一层传入元素位置 i+1；

3.回溯到上一层dfs时，把当前层添加进去的元素（即最后一个元素）删除；

注意点：

1.开始Sort一下，防止因结果乱序判题出错；

2.空集也是子集；

3.结果list中添加子集需要新声明对象；





代码：

```
import java.util.*;
class Solution {
public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        ArrayList<Integer> tmp = new ArrayList();
        Arrays.sort(nums);
        res.add(tmp);
        dfs(nums,res,tmp,0);
        return res;

    }
    public void dfs(int[] nums,List<List<Integer>> res,ArrayList<Integer>  tmp,int pos){
        for(int i=pos;i<nums.length;i++){
            tmp.add(nums[i]);
            res.add(new ArrayList<Integer>(tmp));
            dfs(nums,res,tmp,i+1);
            tmp.remove(tmp.size()-1);
        }
        }
}
```







