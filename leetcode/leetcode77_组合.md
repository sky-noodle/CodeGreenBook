# CodeGreenBook

### Leetcode

[77.组合][https://leetcode-cn.com/problems/combinations/]

给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

示例:

输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/combinations
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

本质上是子集问题，区别在于子集中元素的个数限定为k；

### 算法设计技巧：

1.引入int k 表示当前子集中还需要多少元素；

2.每次dfs，因为加入当前层的元素，因此k-1；

3.dfs的递归跳出条件为k==0；

### 注意点：



代码：

```
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> tmp = new ArrayList<>();
        dfs(res,tmp,n,k,1);
        return res;
    }
    void dfs(List<List<Integer>> res,List<Integer> tmp,int n,int k,int pos){
        if(k==0){
            res.add(new ArrayList<>(tmp));
            return;
        }
        for(int i=pos;i<=n;i++){
            tmp.add(i);
            dfs(res,tmp,n,k-1,i+1);
            tmp.remove(tmp.size()-1);
        }
    }
}

```







