# CodeGreenBook

### Leetcode

[17.电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。



示例:

输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

排列组合思想，先固定第一个字母，dfs向下搜索，直到组成长度为输入数字长度的字符串再回溯；

### 算法设计技巧：

1.设计二维字符数组 table，存储电话按键字符，一维下标表示对应数组，行向量表示当前数字可代表的字母；

2.每次取digits的第一位数字，然后从当前数字对应的行向量从0到尾搜索；

3.进入下层dfs时传入去除第一位数字的digits；

4.递归跳出条件为digits的长度为0；

### 注意点：

1.数字1对应空集；

2.tmp添加字符传入下层递归，不需要再截取；

代码：

```
class Solution {
    public List<String> letterCombinations(String digits) {
        // if(digits==null ||digits.length()==0)
        // return null;
        char[][] table = {{},{'a','b','c'},{'d','e','f'},{'g','h','i'},{'j','k','l'},{'m','n','o'},{'p','q','r','s'},{'t','u','v'},{'w','x','y','z'}};
        List<String> res = new ArrayList<String>();
        if(digits==null ||digits.length()==0)
         return res;
        dfs(digits,table,"",res);
        return res;
    }
    public void dfs(String digits,char[][] table,String tmp,List<String> res){
        if(digits.length()==0){
            res.add(tmp);
            return;
        }
        for(int i=0;i<table[digits.charAt(0)-'0'-1].length;i++){
            dfs(digits.substring(1),table,tmp+table[digits.charAt(0)-'0'-1][i],res);
        }
    }

}

```







