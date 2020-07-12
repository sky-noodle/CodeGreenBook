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
1.循环结束条件,防止死循环；
2.指针变化条件

1. start + 1 < end  
循环跳出条件，如果start==end，在start不可以跳过mid的情景下（会跳过正确答案），会死循环；
例如，start=1，end=2，mid=(1+2)/2=1；
2.start = mid; end = mid;
左右指针变化都为mid；
好处是不会跳过答案；
需要在循环结束后判断下start/end是否为答案，以及数组中是否存在答案；
3.nums[mid] == target；=> end = mid; / start = mid; /return;
当找到目标数时，如果为寻找任意解，则直接return；
如果为first position 则end=mid，在从当前位置的左侧寻找；
如果为last position 则start=mid，在从当前位置的右侧寻找；
4.=>对于后两种情况，因为会出现start/end对应值都为target情况，因此在返回结果时，先比较并return存在顺序；
例如，寻找first position：
if (nums[start] == target) {
	return start;
}
5. mid = start + (end - start) / 2
防止大数溢出

```

#### 4.算法模板

```
int start = 0, end = nums.length - 1;
while (start + 1 < end) {//start +　1 < end 
	int mid = start + (end - start) / 2;
	if (nums[mid] == target) {
		end = mid;
		} else if (nums[mid] < target) {
			start = mid;
		} else {
			end = mid;
		}
}
if (nums[start] == target) {
	return start;
}
if (nums[end] == target) {
	return end;
}

return -1;


```

### 5.例题解析


##### 5.1基础题：











