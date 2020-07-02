# CodeGreenBook

### Leetcode

#### [560. 和为K的子数组](https://leetcode-cn.com/problems/subarray-sum-equals-k/)

给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

示例 1 :

输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
说明 :

数组的长度为 [1, 20,000]。
数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subarray-sum-equals-k
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

定义pre[i]为[0:i]前缀和,j为子数组开始位置;

目地为搜索子数组和为k的个数,即：满足pre[i]-pre[j-1]==k的[j:i]对个数；

边计算边更新hash，则保证hash[pre[j]]更新的j下标满足0<=j<=i;

因此设计命中hash条件为pre[i]-k,(pre[j-1] =pre[i]-k);

每次命中hash表示以i为右边界的子数组，已经存在values个满足条件的数组；

hash的values只关心个数，不关心子数组具体开始位置；

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int subarraySum(int[] nums, int k) {
        if(nums==null||nums.length==0)
            return 0;
        Map<Integer,Integer> map = new HashMap<>();
        int pre=0;
        int res=0;
        map.put(0,1);
        for(int i=0;i<nums.length;i++){
            pre+=nums[i];
            if(map.containsKey(pre-k)){
                res+=map.get(pre-k);
            }
            map.put(pre,map.getOrDefault(pre,0)+1);
        }
        return res;
    }
}

```







