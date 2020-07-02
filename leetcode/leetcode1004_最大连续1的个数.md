# CodeGreenBook

### Leetcode

#### [1004. 最大连续1的个数 III](https://leetcode-cn.com/problems/max-consecutive-ones-iii/)

给定一个由若干 0 和 1 组成的数组 A，我们最多可以将 K 个值从 0 变成 1 。

返回仅包含 1 的最长（连续）子数组的长度。

 

示例 1：

输入：A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
输出：6
解释： 
[1,1,1,0,0,1,1,1,1,1,1]
粗体数字从 0 翻转到 1，最长的子数组长度为 6。
示例 2：

输入：A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
输出：10
解释：
[0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
粗体数字从 0 翻转到 1，最长的子数组长度为 10。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/max-consecutive-ones-iii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 思路：

固定左指针，右指针移动，如果当前元素为0，k--；

每次移动右指针，更新最终结果，直到右指针指向数组尾；

当k<0时表示新加入元素为0，且右指针不能移动；

此时移动左指针，若左指针指向元素为0，则k++；

当k==0时，右指针可以继续右移；



### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int longestOnes(int[] A, int K) {
        if(A==null||A.length==0)
            return 0;
        int res=0;
        int l=0;
        for(int r=0;r<A.length;r++){
            if(A[r]==0)
                K--;
            while (K<0){
                if(A[l]==0)
                    K++;
                l++;
            }
            res = Math.max(res,r-l+1);
        }
        return res;
    }
}
```







