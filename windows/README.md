# CodeGreenBook

## 滑动窗口

#### 定义：

```
借助左右双指针维护一个可滑动的窗口；
利用历史计算结果对搜索空间进行剪枝，减少重复计算；
```

#### 2.应用：

```
解决查找满足一定条件的连续区间性质的问题；
例如满足某条件的最x区间（子串、子序列等）；
```

#### 3.算法设计点：

```
1.设计左右指针移动条件；
2.以多重循环思路模拟算法，考虑重复计算特征，抽象为左指针移动条件；
```

#### 4.算法模板

```
初始化最优解；
int l=0; //
for(int r=0;r<nums.length;r++){
	//更新状态
	while(状态满足条件){
		//更新最优解
		l++;
		//更新状态
	}
}
return 最优解
```

### 5.例题解析


##### 5.1基础题：

[209.长度最小的子数组](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode209_%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.md)

[3.无重复的最长子串](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode3_%E6%97%A0%E9%87%8D%E5%A4%8D%E5%AD%97%E7%AC%A6%E7%9A%84%E6%9C%80%E9%95%BF%E5%AD%90%E4%B8%B2.md)

[1004.最大连续1的个数](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode1004_%E6%9C%80%E5%A4%A7%E8%BF%9E%E7%BB%AD1%E7%9A%84%E4%B8%AA%E6%95%B0.md)

1208.尽可能使字符串相等



##### 5.2困难题目：

340.至少包含K个不同字符的最长子串

1151.最少交换次数来组合所有的1

159.

1100.

