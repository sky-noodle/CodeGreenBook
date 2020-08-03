# CodeGreenBook

### Leetcode

#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：

输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/climbing-stairs
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 思路：

```
state: f[i]表示前i个位置，跳到第i个位置的方案

总数

function: f[i] = f[i-1] + f[i-2]

intialize: f[0] = 1

answer: f[n]
```

### 算法设计技巧：



### 注意点：



代码：

```
public class Solution {
    public int climbStairs(int n) {
        if (n == 0) {
            return 0;
        }
        
        int[] f = new int[n + 1];
        f[0] = 1; 
        f[1] = 1;
        
        for (int i = 2; i <= n; i++) {
            f[i] = f[i - 1] + f[i - 2];
        }
        return f[n];
    }
}

```







