# CodeGreenBook

## DFS-I

#### 定义：

```
深度优先搜索算法（Depth First Search，简称DFS）：一种用于遍历或搜索树或图的算法。 沿着树的深度遍历树的节点，尽可能深的搜索树的分支。当节点v的所在边都己被探寻过或者在搜寻时结点不满足条件，搜索将回溯到发现节点v的那条边的起始节点。整个进程反复进行直到所有节点都被访问为止。属于盲目搜索,最糟糕的情况算法时间复杂度为O(!n)。
```

#### 2.应用：

```
经典的子集、排列、组合问题，以及运筹问题，例如求和、硬币、背包，都可以用dfs求解，本质上是对回溯的应用，对回溯的方向加上深度优先的条件；
```

#### 3.算法设计点：

```
1.问题抽象为dfs求解问题；
2.设计dfs方法的传入参数；
3.设计dfs方法的递归跳出条件；
4.设计标识dfs的遍历对象方法，例如开始位置标识pos，当前元素是否合法的判断函数；
```

#### 4.算法模板

```
class Solution {
    public List<List<Integer>> func(int[] nums) {
    		//res结果集
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        //tmp当前dfs结果
        List<Integer> tmp = new ArrayList<>();
        //排序方便dfs顺序；
        Arrays.sort(candidates);
        //dfs
        dfs(nums,res,tmp,0);
        return res;
    }
    public void dfs(int[] nums,List<List<Integer>> res,List<Integer> tmp,int pos){
    		//递归跳出条件
        if(condition){
            res.add(new ArrayList<>(tmp));
            return;
        }
        //dfs遍历，pos标志当前子集开始位置；
        for(int i=pos;i<candidates.length;i++){
        		//组成tmp候选集
            tmp.add(nums[i]);
            //dfs，下层传入pos+1
            dfs(nums,res,tmp,i+1);
            //删除最近一次元素，回溯
            tmp.remove(tmp.size()-1);
        }
    }
}


```

### 5.例题解析


##### 5.1基础题：

[78.子集](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode78_%E5%AD%90%E9%9B%86.md)

[79.子集II](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode79_%E5%AD%90%E9%9B%86II.md)

[77.组合](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode77_%E7%BB%84%E5%90%88.md)

[46.全排列](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode46_%E5%85%A8%E6%8E%92%E5%88%97.md)

[47.全排列II](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode47_%E5%85%A8%E6%8E%92%E5%88%97II.md)

[59.组合总和](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode59_%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8C.md)

[60.组合总和II](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode60_%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CII.md)

##### 5.2 一维题目

22.括号生成

17.电话号码的字符组合

93.复原ip地址

分割回文串

#### 5.3 二维题目

