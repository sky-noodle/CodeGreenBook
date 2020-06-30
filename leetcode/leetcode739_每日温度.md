# CodeGreenBook

### Leetcode

[739.每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

请根据每日 气温 列表，重新生成一个列表。对应位置的输出为：要想观测到更高的气温，至少需要等待的天数。如果气温在这之后都不会升高，请在该位置用 0 来代替。

例如，给定一个列表 temperatures = [73, 74, 75, 71, 69, 72, 76, 73]，你的输出应该是 [1, 1, 4, 2, 1, 1, 0, 0]。

提示：气温 列表长度的范围是 [1, 30000]。每个气温的值的均为华氏度，都是在 [30, 100] 范围内的整数。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/daily-temperatures
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

递减栈，每次出栈表示当前栈顶元素遇到了更高气温；

当前元素减去栈顶元素即为栈顶元素的最少等待天数；

### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public int[] dailyTemperatures(int[] T) {
        if(T==null ||T.length==0)
            return new int[0];
        int[] res = new int[T.length];
        Stack<Integer> st = new Stack<>();
        for(int i=0;i<T.length;i++){
            while(!st.empty()&&T[i]>T[st.peek()]){
                int top = st.pop();
                res[top]=i-top;
            }
            st.push(i);
        }
        return res;
    }
}

```







