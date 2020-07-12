# CodeGreenBook

### Leetcode

#### [74. 搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix/)

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。
示例 1:

输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
输出: true

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/search-a-2d-matrix
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。





### 思路：

排序矩阵，二分思路；

思路一：现二分行，寻找最后一个<=target的行，表示在此行中；

再二分此行的列；

思路二：二维数组连接成一维有序数组；



### 算法设计技巧：



### 注意点：



代码：

```
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix==null || matrix.length==0 || matrix[0]==null || matrix[0].length==0)
            return false;
        int col = matrix[0].length;
        int row = matrix.length;
        int len = col*row;
        int left = 0;
        int right = len-1;
        int mid=0;
        while (left+1<right){
            mid = (left+right)/2;
            if(matrix[mid/col][mid%col]==target){
                return true;
            }else if(matrix[mid/col][mid%col]>target){
                right = mid;
            }else{
                left = mid;
            }
        }
        if(matrix[left/col][left%col]==target){
            return true;
        }else if (matrix[right/col][right%col]==target){
            return true;
        }
        return false;
    }
}

```







