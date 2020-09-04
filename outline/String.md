# CodeGreenBook

#### [796. 旋转字符串](https://leetcode-cn.com/problems/rotate-string/)

```
给定两个字符串 s1 和 s2，要求判定 s2 是否能够被 s1 做循环移位得到的字符串包含。
s1 = AABCD, s2 = CDAA
Return : true
```

思路：1.先判断长度，不等长一定非旋转

2.拼接A+A，旋转数组一定是子串；

```
class Solution {
    public boolean rotateString(String A, String B) {
        if(A.length() != B.length()){
            return false;
        }
        String allStr = A + A;
        if(allStr.contains(B)){
            return true;
        }
        return false;
    }
}
```

## 字符串循环位移

```
将字符串向右循环移动 k 位。
s = "abcd123" k = 3
Return "123abcd"
```

思路：先翻转abcd、123；再整体翻转

```
    public static String revoStr(String s, int k){
        char[] ch = s.toCharArray();
        swapStr(ch,0,s.length()-k-1);
        swapStr(ch,s.length()-k,s.length()-1);
        swapStr(ch,0,s.length()-1);
        String res = String.valueOf(ch);
        return res;
    }
    private static void swapStr(char[] ch,int start,int end){
        while (start<end){
            char tmp = ch[start];
            ch[start] = ch[end];
            ch[end] = tmp;
            start++;
            end--;
        }
    }
```

#### [151. 翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

```
输入: "the sky is blue"
输出: "blue is sky the"
```

思路：先翻转单词，在整体翻转；

```
class Solution {
    public String reverseWords(String s) {
        char[] ch = s.toCharArray();
        int left =0;
        int right = s.length()-1;
        for(int i=0;i<ch.length-1;i++){
            if(ch[i]==' ' && ch[i+1]!=' '){
                swapStr(ch,left,i-1);
                left = i+1;
            }
        }
        swapStr(ch,left,right);
        swapStr(ch,0,right);
        return cleanSpaces(ch, ch.length);
    }
    public static char[] swapStr(char[]ch,int left, int right){
        while (left<right){
            char tmp = ch[left];
            ch[left] = ch[right];
            ch[right] = tmp;
            left++;
            right--;
        }
        return ch;
    }
    private static String cleanSpaces(char[] a, int n) {
        int i = 0, j = 0;
        while (j < n) {
            while (j < n && a[j] == ' ')
                j++;
            while (j < n && a[j] != ' ')
                a[i++] = a[j++];
            while (j < n && a[j] == ' ')
                j++;
            if (j < n)
                a[i++] = ' ';
        }
        return new String(a).substring(0, i);
    }
}

```

#### [242. 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的字母异位词。

```
输入: s = "anagram", t = "nagaram"
输出: true
```

思路：hash计数，遍历s对每个字母出现次数+1，遍历t对每个字母出现次数-1，如果有非0则非异位词；

```
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length()!=t.length()){
            return false;
        }
        char[] ch = new char[26];
        for(int i = 0;i<s.length();i++){
            ch[s.charAt(i)-'a']++;
        }
        for(int i = 0;i<s.length();i++){
            ch[t.charAt(i)-'a']--;
        }
        for(int i=0;i<26;i++){
            if(ch[i]!=0){
                return false;
            }
        }
        return true;
    }
}
```

#### [409. 最长回文串](https://leetcode-cn.com/problems/longest-palindrome/)

给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。

```
输入:
"abccccdd"
输出:
7
```

思路：1.hash计数，遍历一遍字母出现次数计数；

2.对出现偶数次，结果长度+2；

3.最后如果结果长度小于字符串长度，则还可以+1（奇数回文）

```
class Solution {
    public int longestPalindrome(String s) {
        if(s==null || s.length()==0){
            return 0;
        }
        char[] ch = new char[256];
        for(int i=0;i<s.length();i++){
            ch[s.charAt(i)]++;
        }
        int count=0;
        for(int i=0;i<ch.length;i++){
            count+=(ch[i]/2)*2;
        }
        if(count<s.length()){
            count++;
        }
        return count;
    }
}
```

#### [205. 同构字符串](https://leetcode-cn.com/problems/isomorphic-strings/)

```
输入: s = "egg", t = "add"
输出: true
```

思路：遍历s，以s与t的相同下标记录对应字符的出现次数；如果次数不一致则表示非同构；

```
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if(s.length()!=t.length()){
            return false;
        }
        int[] ch1 = new int[256];
        int[] ch2 = new int[256];
        for(int i =0;i<s.length();i++){
            char chs = s.charAt(i);
            char cht = t.charAt(i);
            if(ch1[chs]!=ch2[cht]){
                return false;
            }
            ch1[chs] = i+1;
            ch2[cht] = i+1;
        }
        return true;
    }
}
```

#### [647. 回文子串](https://leetcode-cn.com/problems/palindromic-substrings/)

给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。

思路：中心展开思想，对每个位置向两侧展开，寻找回文子串；奇数偶数分开计算；

```
class Solution {
    private int count = 0;
    public int countSubstrings(String s) {
        char[] ch = s.toCharArray();
        for(int i=0;i<ch.length;i++){
            isPair(ch,i,i);
            isPair(ch,i,i+1);
        }
        return count;
    }
    public  int isPair(char[] ch,int left,int right){
        //int count=0;
        while (left>=0 && right<ch.length && ch[left]==ch[right]){
            count++;
            left--;
            right++;
        }
        return count;
    }
}
```

#### [9. 回文数](https://leetcode-cn.com/problems/palindrome-number/)

```
输入: 121
输出: true
```

思路：对原数除10，在对新数*10，生成右侧数的翻转数；比较二者是否相等；考虑奇数偶数回文；

```
class Solution {
    public boolean isPalindrome(int x) {
        if(x==0){
            return true;
        }
        if(x<0||x%10==0){
            return false;
        }
        int right = 0;
        while (x>right){
            right = right*10 + x%10;
            x=x/10;
        }
        return x==right || x==right/10;
    }
}
```

#### [696. 计数二进制子串](https://leetcode-cn.com/problems/count-binary-substrings/)

```
计算具有相同01个数的子串个数
输入: "00110011"
输出: 6
```

思路：只有01两种字符，因此遍历，计数当前字符出现次数，直到遇到不同字符；更新前一字符次数，当前字符从1开始计数；如果前一字符个数大于等于当前字符则子串数+1；

例如0001，3>1,包含01因此子串数+1；

```
class Solution {
    public int countBinarySubstrings(String s) {
        int count = 0;
        int pre = 0;
        int cur = 1;
        for(int i=1;i<s.length();i++){
            if(s.charAt(i)==s.charAt(i-1)){
                cur++;
            }else{
                pre = cur;
                cur = 1;
            }
            if(pre>=cur){
                count++;
            }
        }
        return count;
    }
}
```

## 回文子串系列

#### [5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

思路：由于是具体解，因此非动态规划问题，中心展开思路，O(n2)复杂度；

外层遍历字符串，内层以为起点向两侧扩展，寻找回文子串；

奇偶分开计算，取最长值；

最优解：马拉车算法

```
class Solution {
    public String longestPalindrome(String s) {
        if(s==null||s.length()<=0)
            return s;
        char[] ch = s.toCharArray();
        int max = 0;
        int len = 0;
        int start = 0;
        int end = 0;
        String res = null;
        for(int i=0;i<s.length();i++){
            start = i;
            end = i;
            while (start>=0 && end<ch.length && ch[start]==ch[end]){
                start--;
                end++;
            }
            len =end-start-1;
            if(len>max){
                res = s.substring(start+1,end);
                max = len;
            }
            start = i;
            end = i+1;
            while (start>=0 && end<ch.length && ch[start]==ch[end]){
                start--;
                end++;
            }
            len =end-start-1;
            if(len>max){
                res = s.substring(start+1,end);
                max = len;
            }
        }
        return res;
    }
}
```

