# CodeGreenBook

#### [136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

思路：异或 （不进位加法)

a^a=0 ;a^0=a

```
class Solution {
    public int singleNumber(int[] nums) {
        if(nums==null || nums.length==0){
            return 0;
        }
        int n = nums[0];
        for(int i =1;i<nums.length;i++){
            n = n^nums[i];
        }
        return n;
    }
}
```

#### [137. 只出现一次的数字 II](https://leetcode-cn.com/problems/single-number-ii/)

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

```
class Solution {
    public int singleNumber(int[] nums) {
        if(nums==null || nums.length==0){
            return 0;
        }
        Map<Integer,Integer> map = new HashMap<>();
        for(int i:nums){
            map.put(i,map.getOrDefault(i,0)+1);
        }
        for(int i:map.keySet()){
            if(map.get(i)==1){
                return i;
            }
        }
        return 0;
    }
}
```

```
class Solution {
  public int singleNumber(int[] nums) {
    int seenOnce = 0, seenTwice = 0;

    for (int num : nums) {
      // first appearence: 
      // add num to seen_once 
      // don't add to seen_twice because of presence in seen_once

      // second appearance: 
      // remove num from seen_once 
      // add num to seen_twice

      // third appearance: 
      // don't add to seen_once because of presence in seen_twice
      // remove num from seen_twice
      seenOnce = ~seenTwice & (seenOnce ^ num);
      seenTwice = ~seenOnce & (seenTwice ^ num);
    }

    return seenOnce;
  }
}

```

#### [260. 只出现一次的数字 III](https://leetcode-cn.com/problems/single-number-iii/)

给定一个整数数组 `nums`，其中恰好有两个元素只出现一次，其余所有元素均出现两次。 找出只出现一次的那两个元素。

思路：2n+2中找不重复的两个数；

先异或一遍，值为两个不重复数的异或值；

利用x&（-x）找二进制最右侧一位1 diff；

根据diff将原来数据分为两类，一类是为1的一类为0，两个不重复数字在两类内；

实现上，只需将diff为0的一类进行累异或便得到其中一个数字n1，n1与diff异或即为n2；

```
class Solution {
    public int[] singleNumber(int[] nums) {
        int[] res = new int[2];
        if(nums==null || nums.length==0){
            return res;
        }
        int n = nums[0];
        for(int i=1;i<nums.length;i++){
            n = n^nums[i];
        }
        int diff = n&(-n);
        int n1 = 0;
        for(int i:nums){
            if((i&diff)!=0){
                n1=n1^i;
            }
        }
        res[0]=n1;
        res[1]=n1^n;
        return res;
    }
}
```

#### [169. 多数元素](https://leetcode-cn.com/problems/majority-element/)

给定一个大小为 *n* 的数组，找到其中的多数元素。多数元素是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

思路：抵消，维护一个元素的集合，遍历数组如果有相同元素计数器加一，否则减一，如果计数器为0重新添加新元素；

因为最终寻找元素严格大于数组长度一半，所以集合最后剩下的元素便是解；

```
import java.util.Arrays;
class Solution {
    public int majorityElement(int[] nums) {
        int pre = 0;
        int count=0;
        for(int i=0;i<nums.length;i++){
            if(count==0){
                pre = nums[i];
                count++;
            } else {
                if(pre==nums[i]){
                    count++;
                }else{
                    count--;
                }
            }
        }
        return pre;
    }
}
```



#### [53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

```
输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
[-2,-1,-4,0,-1,1,3,-2,2]
思路：遍历的时候更新子序列和，如果和小于0，则代表需要重新开始新的子序列加和；
同时max变量存储全局最大值；
dp：dp[i]代表以结尾的子序列最大和；
状态转移为去加上当前num[i]的子序列和已经重新计数的子序列和的较大者；
dp[i] = Math.max(dp[i-1]+nums[i],nums[i])
```



```
public int maxSubArray(int[] nums) {
    if (nums == null)
        return 0;
    int len = nums.length;
    int max = nums[0];
    int sum = 0;
    for(int i=0;i<len;i++) {
        sum=sum+nums[i];
        if(max<sum)
            max=sum;
        if(sum<0)
            sum=0;
    }
    return max;
}
```

```
class Solution {
    public int maxSubArray(int[] nums) {
        int[] dp = new int[nums.length];
        dp[0]=nums[0];
        int res = nums[0];
        for(int i=1;i<nums.length;i++){
            dp[i] = Math.max(dp[i-1]+nums[i],nums[i]);
            res = Math.max(dp[i],res);
        }
        return res;
    }
}
```

#### [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

```
输入: [7,1,5,3,6,4]
输出: 5
思路：前缀和思想，遍历一遍，每个当前元素减去当前最小值，得到类似前缀和数组，对该数组取最大值即可；
```

```
class Solution {
    public int maxProfit(int[] prices) {
        if(prices==null || prices.length==0){
            return 0;
        }
        int[] pix = new int[prices.length];
        int min=prices[0];
        int res=0;
        for(int i=1;i<prices.length;i++){
            if(prices[i]>min){
                pix[i] = prices[i]-min;
            }else{
                pix[i]=0;
            }
            min = Math.min(min,prices[i]);
            res = Math.max(res,pix[i]);
        }
    return res;
    }
}
```

本题不需考虑严格的当前最优买卖数组，因此可化简为：

```
class Solution {
    public int maxProfit(int[] prices) {
      if(prices==null||prices.length==0)
    		return 0;
    	int len = prices.length;
    	int max=0;
    	int res = Integer.MAX_VALUE;
    	for(int i=0;i<len;i++) {
    		res = Math.min(prices[i], res);
    		max = Math.max(max, prices[i]-res);
    	}
    	return max;
    }
}
```



#### [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

```
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 
思路：贪心，只要有收益就买卖
```

```
class Solution {
    public int maxProfit(int[] prices) {
        if(prices==null||prices.length==0)
            return 0;
        int len = prices.length;
        int res = 0;
        for(int i=1;i<len;i++){
            if(prices[i]>prices[i-1]){
                res+=prices[i]-prices[i-1];
            }
        }
        return res;
    }
}
```



#### [123. 买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

```
输入: [3,3,5,0,0,3,1,4]
输出: 6
最多买卖两次，无相交
思路：第一次遍历，维护一个数组pix，描述的是到i为止，一次买卖最大收益；
第二次遍历，从后往前寻找最优两次买卖分割处，满足，当前最大买入值-当前卖出值-截止当前之前的买卖最大收益；
```

```
class Solution {
    public int maxProfit(int[] prices) {
         if(prices==null||prices.length==0)
            return 0;
        int len = prices.length;
        int min = prices[0];
        int[] pix = new int[len];
        pix[0]=0;
        for(int i=1;i<len;i++){
            pix[i] = Math.max(pix[i-1],prices[i]-min);
            min = Math.min(min,prices[i]);
        }
        int sell = prices[len-1];
        int best = 0;
        for(int i=len-2;i>=0;i--){
            best = Math.max(best,sell-prices[i]+pix[i]);
            sell = Math.max(sell,prices[i]);
        }
        return best;
    }
}
```

### 44. 最小子数组

```
给定一个整数数组，找到一个具有最小和的连续子数组。返回其最小和。
输入：[1, -1, -2, 1]
输出：-3
思路：！！！把max subarray 置反

```

```
    public int minSubArray(List<Integer> nums) {
        // write your code here
        if(nums==null || nums.size()==0){
            return 0;
        }
        int max = -nums.get(0);
        int sum = 0;
        for(int i=0;i<nums.size();i++){
           nums.set(i, -nums.get(i));
           sum = nums.get(i)+sum;
           max = Math.max(max,sum);
           if(sum<0) {
               sum = 0;
           }
        }
        return -max;
    }
```

### 子数组之和

```
给定一个整数数组，找到和为 00 的子数组。你的代码应该返回满足要求的子数组的起始位置和结束位置
输入: [-3, 1, 2, -3, 4]
输出: [0,2] 或 [1,3]	
样例解释： 返回任意一段和为0的区间即可。
思路：
```



```
    public List<Integer> subarraySum(int[] nums) {
        // write your code here
        List<Integer> res = new ArrayList<>();
       if(nums==null||nums.length==0){
           return res;
       }
       int len = nums.length;
       int[] pix = new int[len+1];
       pix[0]=0;
          for(int i=0;i<len;i++){
           pix[i+1]=nums[i]+pix[i];
       }
        Map<Integer,Integer> map = new HashMap<>();
       for(int i=0;i<len+1;i++){
           if(map.containsKey(pix[i])){
               res.add(map.get(pix[i]));
               res.add(i-1);
               return res;
           }else{
               map.put(pix[i],i);
           }
       }
       return res;
    }
```

