# CodeGreenBook

### Leetcode

[46.全排列][https://leetcode-cn.com/problems/permutations/]

给定一个 没有重复 数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/permutations
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 思路：

全排列是经典的DFS求解问题，每次从输入序列中选择一个元素，添加到临时子集tmp，知道临时子集的元素个数与序列长度相同，算一次排列；删除最近添加进来的元素进行回溯，组成不同的子集；

以123为例：

第一轮：1 2 3；//dfs到最深

第二轮 ：1 3 2;//回溯到1开头子集，候选元素为 2 3 ，选择3 2；

第三轮：2 1 3；//以1开始的子集遍历完成，以2开始进行dfs，候选集为1 3；

第四轮：2 3 1；//回溯到2开头子集，候选元素为 1 3 ，选择3 1；

第五轮：3 1 2；//以2开始的子集遍历完成，以3开始进行dfs，候选集为1 2；

第六轮：3 2 1；//回溯到3开头子集，候选元素为 1 2 ，选择2 1；

### 算法设计技巧：

1.每次不能从pos开始往后遍历了，因为是全部元素的排列序列，因此每次dfs是从输入序列的第一个元素开始；

2.引入与输入等长的visit数组，标识每个元素是否已经加入tmp；

3.dfs的递归跳出条件为tmp的大小等于输入序列长度；

### 注意点：

1.每次dfs，visit判断是包含for循环内的所有操作，如果已经visit则需跳过；

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
            }
        }
    }
    
}

```







