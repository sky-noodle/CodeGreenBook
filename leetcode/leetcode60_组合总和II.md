# CodeGreenBook

### Leetcode

[40.组合总和][https://leetcode-cn.com/problems/combination-sum-ii/]

给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

说明：

所有数字（包括目标数）都是正整数。
解集不能包含重复的组合。 
示例 1:

输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]

**示例 2:**

```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```

### 思路：

增加了重复元素，与子集II相同的解决思路；

### 算法设计技巧：



### 注意点：

1.每个数字只使用一次，因此下一层dfs的pos应该+1；

代码：

```
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> tmp = new ArrayList<>();
        Arrays.sort(candidates);
        dfs(candidates,res,tmp,target,0);
        return res;
    }
    public void dfs(int[] candidates,List<List<Integer>> res,List<Integer> tmp,int target,int pos){
        if(target==0){
            res.add(new ArrayList<>(tmp));
            return;
        }
        if(target<0){
            return;
        }
        for(int i=pos;i<candidates.length;i++){
            tmp.add(candidates[i]);
            dfs(candidates,res,tmp,target-candidates[i],i+1);
            tmp.remove(tmp.size()-1);
            while(i<candidates.length-1 && candidates[i]==candidates[i+1]) i++;
        }
    }
}
```







