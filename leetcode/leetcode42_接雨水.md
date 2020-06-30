# CodeGreenBook

### Leetcode

[42.接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

给定 *n* 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rainwatertrap.png)

上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 感谢 Marcos 贡献此图。

示例:

输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/trapping-rain-water
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

维护非递增栈，当元素小于等于栈顶元素时，代表雨水块的左界限为栈顶元素，入栈；

当元素大于栈顶元素时，代表雨水块的右界限为当前元素，出栈；

出栈计算雨水块面积，宽度为当前元素下标-1-出栈后的栈顶元素；

高度分两种情况：

1.左界限与右界限之间没有第二层雨水，例如1，0，2；

2.左界限与右界限之间存在两层，例如2，1，0，1，3；

第一种情况，高度为左右界限的最低值；

第二种情况，3，2之间的雨水在0出栈时会累加1*1，

在右侧1出栈时，因为栈顶元素是左侧1，非栈底，因此再次出栈，

高度为右界限与左界限的最小值减去栈顶元素；

### 算法设计技巧：



### 注意点：

出栈时可能会出现空栈

代码：

```
class Solution {
    public int trap(int[] height) {
        if(height==null||height.length==0)
            return 0;
        Stack<Integer> st = new Stack<>();
        int res=0;
        for(int i=0;i<height.length;i++){
            while (!st.empty()&&height[i]>height[st.peek()]){
                int top = st.pop();
                if(st.isEmpty()){
                    break;
                }
                int wid = i-st.peek()-1;
                int he = Math.min(height[i],height[st.peek()]);
                int bhe=he-height[top];
                res+=bhe*wid;
            }
            st.push(i);
        }
        return res;
    }
}

```







