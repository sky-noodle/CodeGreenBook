# CodeGreenBook

 1.XGBoost原理

2.分类器结果大多给0，怎么处理；

3.auc0附近震荡原因；

4.样本不均衡怎么处理；

改目标函数；

5.推荐系统相关：召回、rank方法

编程：

1.最长上升子序列；

        for(int i=0;i<len;i++){
            dp[i]=1;
            for(int j=0;j<i;j++){
                if(nums[j]<nums[i]){
                    dp[i] = Math.max(dp[i],dp[j]+1);
                }
            }
            max = Math.max(max,dp[i]);
        }
2.最大字典序子序列；

从后往前找，最后一个肯定是，找比当前元素大的；

