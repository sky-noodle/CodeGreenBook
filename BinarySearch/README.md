# CodeGreenBook

## 二分查找

#### 定义：

```
对于排序的数组，每次选取中间元素去判断下一次寻找在左半部分还是右半部分，直到不可分割；
思路很简单，细节是魔鬼
```

#### 2.应用：

```

```

#### 3.算法设计点：

```
1.防止死循环；
2.循环结束条件
3.指针变化条件
```

#### 4.算法模板

```
int start = 0, end = nums.length - 1;
while (start + 1 < end) {//start +　1 < end 
	int mid = start + (end - start) / 2;//处理整数溢出
	if (nums[mid] == target) {
		start = mid;
		} else if (nums[mid] < target) {
			start = mid;
		} else {
			end = mid;
		}
}
if (nums[end] == target) {
	return end;
}
if (nums[start] == target) {
	return start;
}
return -1;

1. start + 1 < end
2. start + (end - start) / 2
3. A[mid] ==, <, >
4. A[start] A[end] ? target
```

### 5.例题解析


##### 5.1基础题：











