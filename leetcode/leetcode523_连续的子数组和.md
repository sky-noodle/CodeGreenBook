# CodeGreenBook

### Leetcode

#### [523. 连续的子数组和](https://leetcode-cn.com/problems/continuous-subarray-sum/)

给定一个包含 非负数 的数组和一个目标 整数 k，编写一个函数来判断该数组是否含有连续的子数组，其大小至少为 2，且总和为 k 的倍数，即总和为 n*k，其中 n 也是一个整数。

 

示例 1：

输入：[23,2,4,6,7], k = 6
输出：True
解释：[2,4] 是一个大小为 2 的子数组，并且和为 6。
示例 2：

输入：[23,2,6,4,7], k = 6
输出：True
解释：[23,2,6,4,7]是大小为 5 的子数组，并且和为 42。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/continuous-subarray-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 思路：

设计前缀和hash结构，由于题目是整除问题，考虑取余特性；

hash每次加入的是对k取余后的结果；



1.key为sum%k，value为子数组的左index；

2.考虑前缀和满足整除k条件，即(a[j]-a[i])%k=0;

假设a[i]=x，a[j]=x+n * k;

2.考虑，如果命中，hash取得key，value







假设以i为左指针，j为右指针的子数组，如果子数组和为k的倍数，

//则需要pre[j]=(pre[i]+n * k)%k;



存在性质：

######











### 算法设计技巧：

//倍数条件考虑取余特性：(x+n*k)%k=x%k;



### 注意点：



代码：

```
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        int sum = 0;
        HashMap < Integer, Integer > map = new HashMap< >();
        map.put(0, -1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (k != 0)
                sum = sum % k;
            if (map.containsKey(sum)) {
                if (i - map.get(sum) > 1)
                    return true;
            } else
                map.put(sum, i);
        }
        return false;
    }
}
```







