# CodeGreenBook

### Leetcode



[39.组合总和][https://leetcode-cn.com/problems/combination-sum/]

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 
示例 1:

输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
示例 2:

输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/combination-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

运用子集的思路，找到满足和条件的子集作为结果；

### 算法设计技巧：

需要设计递归传入参数和跳出条件；

1.传入target变量，表示当前为满足和条件，还需多少；

2.当target<0，表示无解，跳出递归；

3.当target==0，表示当前为有效子集，添加res并跳出递归；

### 注意点：

1.需要使用pos标志每次dfs遍历的开始位置，否则会出现重复子集，例如2+3与3+2的和都为5；



代码：

```
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
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
            dfs(candidates,res,tmp,target-candidates[i],i);
            tmp.remove(tmp.size()-1);
        }
    }
}

```







