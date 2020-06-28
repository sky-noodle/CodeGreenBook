# CodeGreenBook

### Leetcode

[22.括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

 

示例：

输入：n = 3
输出：[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/generate-parentheses
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

基于数字组合思路，需要确定什么情况下括号是合法的；

分析：括号是成对存在，且左括号在前，左括号数始终大于等于右括号；

1.如果左括号还没添加完，则可以继续添加；

2.如果已经添加的左括号数大于右括号，则可以添加右括号；

因此dfs先放置左括号，满足条件再放置右括号；

### 算法设计技巧：



### 注意点：



代码：

```

class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        if(n<=0)
            return res;
        dfs(res,"",n,n);
        return res;
    }
    public void dfs(List<String> res,String tmp,int left,int right){
        if(left==0&&right==0){
            res.add(tmp);
            return;
        }
        if(left>0){
            //String ntmp = tmp+"(";
            tmp = tmp+"(";
            dfs(res,tmp,left-1,right);
            tmp =  tmp.substring(0,tmp.length()-1);
        }
        if(right>left){
            tmp = tmp+")";
            dfs(res,tmp,left,right-1);
            tmp = tmp.substring(0,tmp.length()-1);
        }
    }
    
}
```







