# CodeGreenBook

### Leetcode

[93.复原ip地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

有效的 IP 地址正好由四个整数（每个整数位于 0 到 255 之间组成），整数之间用 '.' 分隔。

 

示例:

输入: "25525511135"
输出: ["255.255.11.135", "255.255.111.35"]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/restore-ip-addresses
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

ip地址分为4段，每段范围0-255，每段可能1、2、3个字符组成=>转化为组合问题；

### 算法设计技巧：

1.每次dfs从第一个字符往后取3个字符，如果为合法ip段则进入下层dfs，ip段计数器count++；

2.下层dfs传入切割上层ip段的字符串s；

3.递归跳出条件为count==3且剩下的字符串s为合法ip段；

### 注意点：

1.验证ip段是否合法时，'001'等以'0'开头但是非0值都非法；

2.取ip段时，不但i<4同时，由于s每次dfs都进行了切片，因此也要考虑s长度；

3.Integer.parseInt(s); //字符串转成十进制数

代码：

```
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<String>();
        if(s.length()<4 || s.length()>12)
            return res;
        dfs(s,"",res,0);
        return res;
    }
    void dfs(String s,String tmp,List<String>  res,int count){
        if(count==3 && isIP(s)){
            res.add(tmp+s);
            return;
        }
        for(int i=1;i<4&&i<s.length();i++){
            String sub = s.substring(0,i);
            if(isIP(sub)) {
                dfs(s.substring(i), tmp + sub + '.', res, count+1);
            }
        }
    }
    boolean isIP(String s){
        if(s.charAt(0)=='0')
            return s.equals("0");
        int num = Integer.parseInt(s); //字符串转成十进制数
        return num<=255 && num>0;
    }
}

```







