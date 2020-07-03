# CodeGreenBook

## 前缀和

#### 定义：

```
前缀和数组prefixSum，长度为nums.length+1，数据nums的累加依次放入prefixSum中；
例如：
prefixSum[0]=0;
prefixSum[1]=sum[0];
prefixSum[2]=prefixSum[1]+sum[1];
...
=>前缀和数组性质：
1.nums[x]=prefixSum[x]-prefixSum[x-1];
2.子数组元素和=prefixSum[right+1]-prefixSum[left];

```

#### 2.应用：

```
数据预处理，用于降低查询时间，通常结合Hash，降低时间复杂度；
解决连续子数组类问题；
```

#### 3.算法设计点：

```
1.只引入前缀和数组算法思路清晰，只需考虑子数组满足条件即可；
2.算法设计复杂在于hash表的结合，边计算前缀和边构建hash；
hash需要设计=>
key：前缀和；
value：前缀和出现多少次；
设计命中hash的条件；
```

#### 4.算法模板

```
	//map构建hash
	Map<Integer,Integer> map = new HashMap<>();
	int pre=0;//前缀和
	int res=0;//最终结果
	map.put(0,1);//加入（0，1）表示前缀和出现一次
	//遍历数组
	for(int i=0;i<nums.length;i++){
		pre+=nums[i];//计算当前前缀和
		//命中hash后更新最终结果
		if(map.containsKey(命中条件)){
			res+=map.get(命中key);
		}
		//更新map，如果没有命中则加入(pre,1),命中则原values+1
		map.put(pre,map.getOrDefault(pre,0)+1);
	}
	return res;
```

### 5.例题解析


##### 5.1基础题：



[560.和为K的子数组](https://github.com/sky-noodle/CodeGreenBook/blob/master/leetcode/leetcode560_%E5%92%8C%E4%B8%BAK%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.md)

523.

974.





