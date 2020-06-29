# CodeGreenBook

输入：数组；

输出：数组中每个元素向右走遇到第一个比自己大的距离；

示例：

输入：[5，3，1，2，4]

输出：[-1，3，1，1，-1]



### 思路：

stack中存储的是原数组的index；

遍历数组，当遇到比栈顶元素大的数时，弹出栈内所有对应数比当前元素小的元素，并更新结果数组；

因为栈的单调性，栈顶元素比当前元素大，代表栈内所有元素都比当前元素大；

对于栈内的每个元素，当出栈时代表遇到了右侧最近的比自己大元素，因此更新距离为i-top；

如果元素没有出栈则代表右侧无比自己大元素；

### 算法设计技巧：



### 注意点：



代码：

```
public int[] nextExceed(int [] input){
	int [] res = new int[input.length];
	Arrays.fill(res,-1);
	Stack<Integer> st = new Stack<>();
	for(int i=0;i<input.length;i++){
		while(!st.empty()&&input[i]>input[st.peek()])
			int top = st.pop();
			res[top]=i-top;
	}
	st.push(i);
}

```







