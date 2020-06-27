# CodeGreenBook

### Leetcode

[47.全排列II][https://leetcode-cn.com/problems/permutations-ii/]

给定一个可包含重复数字的序列，返回所有不重复的全排列。

示例:

输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/permutations-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

46.全排列的补充题，增加了重复元素，与79.子集II一样解决思路，在remove后增加判断，如果重复元素跳过；

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        ArrayList<Integer> tmp = new ArrayList<>();
        Arrays.sort(nums);
        boolean [] visit = new boolean[nums.length];
        dfs(nums,res,tmp,visit);
        return  res;
    }
    public void dfs(int[] nums,List<List<Integer>> res,ArrayList<Integer> tmp,boolean [] visit){
        if(tmp.size()==nums.length){
            res.add(new ArrayList<>(tmp));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if(visit[i]==false){
                tmp.add(nums[i]);
                visit[i]=true;
                dfs(nums,res,tmp,visit);
                tmp.remove(tmp.size()-1);
                visit[i]=false;
                while (i<nums.length-1&&nums[i]==nums[i+1]) i++;
            }
        }
    }
    
}

```







