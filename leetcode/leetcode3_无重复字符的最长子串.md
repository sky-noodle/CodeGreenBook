# CodeGreenBook

### Leetcode

#### [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

左右双指针滑动窗口；

固定左指针，滑动右指针，当右指针指向元素不包含在当前窗口内，右指针++；

否则计算当前窗口长度，更新最优解；

计算左指针滑动位置，为左指针位置和窗口内重复元素下一个元素的对比更靠右边位置；

### 算法设计技巧：

1.字符重复类问题，引入int[128] hash，简单的ASCII哈希，计算是否重复；

2.字符可作为hash数组下标，因为char可隐式转化为int，值为ASCII值；

### 注意点：



代码：

```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s==null || s.length()==0)
            return 0;
        int l = 0;
        int[] hash = new int[128];
        Arrays.fill(hash,-1);
        int res=0;
        for(int r=0;r<s.length();r++){
            char cur = s.charAt(r);
            if(hash[cur]!=-1){
                l = Math.max(l,hash[cur]+1);
            }
            res = Math.max(res,r-l+1);
            hash[cur]=r;
        }
        return res;
    }
}

```







