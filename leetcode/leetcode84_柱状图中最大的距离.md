# CodeGreenBook

### Leetcode

[84.柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

给定 *n* 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。



![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 `[2,1,5,6,2,3]`。

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram_area.png)



图中阴影部分为所能勾勒出的最大矩形面积，其面积为 `10` 个单位。

 

**示例:**

```
输入: [2,1,5,6,2,3]
输出: 10
```

### 思路：

把-1压入栈代表栈底；

从左遍历压栈，直到遇到非递增柱；

出栈，直到满足递增；

每次出栈，用出栈元素作为高，宽为当前元素与当前栈顶元素距离-1；

如果遍历完，栈顶不为-1，表示栈中存在递增序列，还需要出栈；



解释：

元素出栈表示我们已经计算了以出栈元素为高的最大矩形面积；

理解宽度：for循环指针始终比top指针大1，因此i-1，

因为出栈的元素一定比新入栈元素大，如果之前存在出栈元素，则宽度为本身1+之前删除的元素=>i-1-st.peek();

例如：[6,8,7]=>[6,7,5]

7<8，8出栈，res=8*2-1-0=8；

5<7，7出栈，res=7*3-1-0=14；

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int largestRectangleArea(int[] heights) {
        if(heights.length==0)
            return 0;
        Stack<Integer> st = new Stack<>();
        st.push(-1);
        int res=Integer.MIN_VALUE;

        for(int i=0;i<heights.length;i++){
            while (st.peek()!=-1&&heights[st.peek()]>heights[i]){
                int top = st.pop();
                int width = i-st.peek()-1;
                res = Math.max(res,heights[top]*width);
            }
            st.push(i);
        }
        while (st.peek()!=-1){
            int top = st.pop();
            res = Math.max(res,heights[top]*(heights.length-1-st.peek()));
        }
        return res;
    }
}

```







