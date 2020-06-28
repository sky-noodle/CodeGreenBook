# CodeGreenBook

### Leetcode

[131.分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/)

给定一个字符串 s，将 s 分割成一些子串，使每个子串都是回文串。

返回 s 所有可能的分割方案。

示例:

输入: "aab"
输出:
[
  ["aa","b"],
  ["a","a","b"]
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/palindrome-partitioning
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

类似子集和ip问题，原字符串分割成任意个子集，保证每个子集为回文串；

每个子集从当前字符开始搜索，不限长；

### 算法设计技巧：

1.回文字符串的判断，首尾指针同时往中间走，避免区别奇数/偶数情况；

### 注意点：



代码：

```
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<List<String>>();
        List<String> tmp = new ArrayList<>();
        dfs(s,res,tmp);
        return res;
    }
    void dfs(String s,List<List<String>> res, List<String> tmp){
        if(s.length()==0) {
            res.add(new ArrayList<>(tmp));
            //return;
        }
        for(int i=1;i<=s.length();i++){
            String sub = s.substring(0,i);
            if(isPal(sub)){
                tmp.add(sub);
                dfs(s.substring(i),res,tmp);
                tmp.remove(tmp.size()-1);

            }
        }
    }
    boolean isPal(String s){
        int l=0;
        int r=s.length()-1;
        while (l<r){
            if(s.charAt(l++)!=s.charAt(r--))
                return false;
        }
        return true;
    }
    
}

```







