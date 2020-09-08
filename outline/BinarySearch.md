# BinarySearch

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

模板解析：

1.start+1 < end 表示循环结束条件为start与end相交或相邻；

2.死循环：（死循环情况1.mid计算结果为start，例如(1+2)/2=1；2.后面移动为start=mid；3.循环结束条件为start与end相交）；

3.内部 start/end = mid，不+1不会漏解；

4.循环结束后，start与end可能不等，因此需要判断下二者谁为解；

5.nums[mid] == target，如果任何位置，return mid ，如果第一位置end = mid，如果最后位置，start=mid；

### 寻找有序数组特定元素的开始和结束位置

```
 public static int[] searchRange(int[] nums,int target){
        int[] res = new int[2];
        if(nums==null || nums.length==0){
            return res;
        }
        res[0] = findFirst(nums, target);
        res[1] = findLast(nums, target);
        return res;
    }
    public static int findFirst(int[] nums, int target){
        int start = 0;
        int end = nums.length-1;
        int mid = 0;
        while (start+1<end){
            mid = start + (end-start)/2;
            if(nums[mid]==target){
                end = mid;
            }else if(nums[mid]<target){
                start=mid;
            }else {
               end=mid;
            }
        }
        if(nums[start]==target){
            return start;
        }
        if(nums[end]==target){
            return end;
        }
        return -1;
    }
    public static int findLast(int[] nums, int target){
        int start = 0;
        int end = nums.length-1;
        int mid = 0;
        while (start+1<end){
            mid = start + (end-start)/2;
            if(nums[mid]==target){
                start = mid;
            }else if(nums[mid]<target){
                start=mid;
            }else {
                end=mid;
            }
        }
        if(nums[end]==target){
            return end;
        }
        if(nums[start]==target){
            return start;
        }
        return -1;
    }
```

#### [35. 搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

输入: [1,3,5,6], 5 输出: 2 

```
    public int searchInsert(int[] nums, int target) {
        int res =0;
        if(nums==null || nums.length==0)
            return res;
        int len = nums.length;
        int left=0;
        int right=len-1;
        int mid=0;
        while (left+1<right){
            mid = left+(right-left)/2;
            if(nums[mid]==target)
                return mid;
            else if(nums[mid]>target){
                right=mid;
            }else{
                left=mid;
            }
        }
        if(nums[left]>=target){
            res=left;
        }
        else if(nums[right]>=target){
            res=right;
        }else{
            return len;
        }
        return res;
    }
```

#### [74. 搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix/)

matrix = [ [1, 3, 5, 7], [10, 11, 16, 20], [23, 30, 34, 50] ] target = 3 输出: true

```
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
```

#### [278. 第一个错误的版本](https://leetcode-cn.com/problems/first-bad-version/)

```
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int start =0;
        int end = n;
        while(start+1<end){
            int mid = start + (end-start)/2;
            if(isBadVersion(mid)==true){
                end = mid;
            }else{
                start = mid;
            }   
        }
        if(isBadVersion(start)==true)
            return start;
        return end;
    }
```

#### [162. 寻找峰值](https://leetcode-cn.com/problems/find-peak-element/)

```
    public int findPeakElement(int[] nums) {
        if(nums==null || nums.length==0)
        return 0;
        int left = 0;
        int right = nums.length-1;
        int mid=0;
        while(left+1<right){
            mid = (right+left)/2;
            if(nums[mid]>nums[mid-1] && nums[mid]>nums[mid+1]){
                return mid;
            }
            if(nums[mid]>nums[mid-1]){
                left = mid;
            }else{
                right = mid;
            }
        }
        if(left==0 && nums[right]<nums[left])
        return 0;
        if(right==nums.length-1 && nums[right]>nums[left])
        return right;

        return 0;
    }
```

#### [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

nums = [4,5,6,7,0,1,2], target = 0 输出: 4 

思路：

1.nums[mid]先跟nums[left]比较，确定mid落在左侧上升数组还是右侧旋转后的上升数组；

2.两段数组分别处理，左侧数组：只有target在left与mid之间，right=mid；否则left=mid，因为此时不确定target是在哪个上升数组；

3.右侧数组同理：只有target在mid与right之间，left=mid；否则right=mid；

4.最后再判断下left与right值；

```
public int search(int[] nums, int target) {
        if(nums==null || nums.length==0)
        return -1;
        int left =0;
        int right = nums.length-1;
        int mid = 0;
        while(left+1<right){
            mid = (left+right)/2;
            if(nums[mid]==target)
                return mid;
            if(nums[mid]>nums[left]){
                if(nums[left]<=target && nums[mid]>=target){
                    right = mid;
                }else{
                    left = mid;
                }
            }else{
                if(target>=nums[mid] && target<=nums[right]){
                    left = mid;

                }else{
                    right=mid;
                }
            }
        }
        if(nums[left] == target){
            return left;
        }
        if(nums[right] == target)
        return right;
        return -1;
    }
```

#### [81. 搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

nums = [2,5,6,0,0,1,2], target = 0

思路：与上题一致，对加入的重复数字做处理，如果nums[left]==nums[mid],则无法判断mid落在哪个数组，此时left++；

```
class Solution {
public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        int left = 0;
        int right = nums.length-1;
        while (left+1 < right){
            int mid = (right+left)/2;
            if(nums[mid]==target){
                return true;
            }
            if(nums[left]==nums[mid]){
                left++;
                continue;
            }
            if(nums[mid]>nums[right]){
                if(nums[left]<=target && nums[mid]>=target){
                    right = mid;
                }else{
                    left=mid;
                }
            }else{
                if(nums[mid]<=target && nums[right]>=target){
                    left=mid;
                }else{
                    right = mid;
                }
            }
        }
        if(nums[left]==target || nums[right]==target){
            return true;
        }
        return false;
    }
}
```

#### [153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

```
class Solution {
    public int findMin(int[] nums) {
        if(nums==null||nums.length==0){
            return -1;
        }
        int left = 0;
        int right = nums.length-1;
        while (left+1<right){
            int mid = (left+right)/2;
            if(nums[mid]>nums[right]){
                left = mid;
            }else{
                right=mid;
            }
        }
        return Math.min(nums[left],nums[right]);
    }
}
```

#### [154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

注意数组中可能存在重复的元素。

```
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length-1;
        while (left+1<right){
            int mid = (left+right)/2;
            if(nums[mid]==nums[right]){
                right--;
            }else if(nums[mid]>nums[right]){
                left = mid;
            }else{
                right=mid;
            }
        }
        return Math.min(nums[left],nums[right]);
    }
    
}
```

#### [4. 寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

思路：

1.二分思想每次删除k/2个值；

```

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null) {
            return 0;
        }
        int len1 = nums1.length;
        int len2 = nums2.length;
        int lenall = len1+len2;
        if(lenall%2==0){
            return (findK(nums1,0,nums2,0,lenall/2)+findK(nums1,0,nums2,0,lenall/2+1))/2.0;
        }else{
            return findK(nums1,0,nums2,0,lenall/2+1);
        }

    }
    public int findK(int[] nums1,int start1,int[] nums2,int start2,int k){
        if(start1>= nums1.length){
            return nums2[start2+k-1];
        }
        if(start2>=nums2.length){
            return nums1[start1+k-1];
        }
        if(k==1){
            return Math.min(nums1[start1],nums2[start2]);
        }
        int value1 = start1+k/2-1< nums1.length ? nums1[start1+k/2-1]:Integer.MAX_VALUE;
        int value2 = start2+k/2-1< nums2.length ? nums2[start2+k/2-1]:Integer.MAX_VALUE;
        if(value1<value2){
            return findK(nums1,start1+k/2,nums2,start2,k-k/2);
        }else{
            return findK(nums1,start1,nums2,start2+k/2,k-k/2);
        }
    }
}
```



#### [88. 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int index1=m-1;
        int index2=n-1;
        for(int i= n+m-1;i>=0;i--){
            if(index1<0){
                nums1[i]=nums2[index2--];
            }else if(index2<0){
                nums1[i]=nums1[index1--];
            }else if(nums1[index1]>=nums2[index2]){
                nums1[i]=nums1[index1];
                index1--;
            }else{
                nums1[i]=nums2[index2];
                index2--;
            }
        }
    }
}
```



#### [796. 旋转字符串](https://leetcode-cn.com/problems/rotate-string/)

```
    public boolean rotateString(String A, String B) {
        if(A.length()!=B.length())
			return false;
		String C= A+A;
		if(C.indexOf(B)!=-1)
			return true;
		return false;
    }
```



#### [151. 翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

```
    public String reverseWords(String s) {
        if(s==null) return null;
        char [] ch = s.toCharArray();
		swap(ch,0,ch.length-1);
		int begin=0;
		for(int i=0;i<ch.length;i++) {
			if(ch[i]==' ') {
				swap(ch,begin,i-1);
				begin=i+1;
			}	
			if(i==ch.length-1) {
				swap(ch,begin,i);
			}	
		}
        
		return cleanSpaces(ch, ch.length);	
	}
	
	public static char[] swap(char[] ch,int left,int right) {
		while(right>left) {
			char tmp = ch[left];
			ch[left]=ch[right];
			ch[right]=tmp;
			left++;
			right--;
		}
		return ch;
	}
    	private String cleanSpaces(char[] a, int n) {
		int i = 0, j = 0;
		while (j < n) {
			while (j < n && a[j] == ' ')
				j++;
			while (j < n && a[j] != ' ')
				a[i++] = a[j++]; 
			while (j < n && a[j] == ' ')
				j++; 
			if (j < n)
				a[i++] = ' '; 
		}
		return new String(a).substring(0, i);
	}
```

