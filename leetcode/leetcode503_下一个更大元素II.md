# CodeGreenBook

### Leetcode

[503.下一个更大元素II](https://leetcode-cn.com/problems/next-greater-element-ii/)

给定一个循环数组（最后一个元素的下一个元素是数组的第一个元素），输出每个元素的下一个更大元素。数字 x 的下一个更大的元素是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 -1。

示例 1:

输入: [1,2,1]
输出: [2,-1,2]
解释: 第一个 1 的下一个更大的数是 2；
数字 2 找不到下一个更大的数； 
第二个 1 的下一个最大的数需要循环搜索，结果也是 2。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/next-greater-element-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

拼接为循环数组，维护递减栈，遇到比栈顶大的元素出栈；

出栈以为到栈顶元素找到更大的数；

注意本题找的是最近的更大数的值不是距离；

### 算法设计技巧：

1.循环数组，需要考虑最后一个元素；

2.循环数据，设计两倍数组拼接，下标计算公式：index = （right-left+M）%M;

例如 1，2，1 => 1，2，1，1，2，1

index=i%len;

### 注意点：



代码：

```

class Solution {
    public int[] nextGreaterElements(int[] nums) {
        if(nums==null || nums.length==0)
            return new int[0];
        int len = 2*nums.length;
        Stack<Integer> st = new Stack<>();
        int[] res = new int[nums.length];
        Arrays.fill(res,-1);
        for(int i=0;i<len;i++){
            int index = i%nums.length;
            while (!st.empty()&&nums[index]>nums[st.peek()]){
                int top = st.pop();
                res[top] = nums[index];
            }
            st.push(index);
        }
        return res;
    }
}
```







