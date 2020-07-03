# CodeGreenBook

## 单调栈

#### 定义：

```
堆栈数据结构，里面的元素按照栈内位置满足一定的单调性；
当单调性被打破时，需要出栈，保证单调性；
```

#### 2.应用：

```
通常解决一维数组，求解问题需要多重遍历，每个元素于前后大小有关系的情况；
例如视野问题、距离问题、柱状图最大面积、接雨水等；
（与动态规划解决问题类似）
```

#### 3.算法设计点：

```
1.栈中存储的通常是数组下标；
2.入栈前会在栈顶把破坏单调性的元素出栈；
2.考虑每个元素出栈时的意义；
2.出栈时要更新结果；
```

#### 4.算法模板

```
stack<> st;
for(int i=0;i<inputs.length;i++)//遍历数组
{
	while(!st.empty() && inputs[st.peek()]<inputs[i])//栈不为空且栈顶元素小于当前元素
	{
		int top = st.pop();//栈顶元素出栈
		res[top]=i-top; //更新结果
	}
	st.push(i)//当前数据入栈

}


```

### 5.例题解析


##### 5.1基础题：

[谷歌面试题-求每个数右边第一大元素距离](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/Goole_interview1.md)



[739.每日温度](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode739_%E6%AF%8F%E6%97%A5%E6%B8%A9%E5%BA%A6.md)

[503.下一个更大元素II](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode503_%E4%B8%8B%E4%B8%80%E4%B8%AA%E6%9B%B4%E5%A4%A7%E5%85%83%E7%B4%A0II.md)

901.股票价格跨度

962.最大宽度坡







84.柱状图中最大的矩形

85.最大矩形面积

42.接雨水

239.滑动窗口最大值



