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

寻找有序数组特定元素的开始和结束位置；

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

```
class Solution {
public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        int start = 0;
        int end = nums.length - 1;
        int mid;
        while (start <= end) {
            mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[start] == nums[mid]) {
                start++;
                continue;
            }
            //前半部分有序
            if (nums[start] < nums[mid]) {
                //target在前半部分
                if (nums[mid] > target && nums[start] <= target) {
                    end = mid - 1;
                } else {  //否则，去后半部分找
                    start = mid + 1;
                }
            } else {
                //后半部分有序
                //target在后半部分
                if (nums[mid] < target && nums[end] >= target) {
                    start = mid + 1;
                } else {  //否则，去后半部分找
                    end = mid - 1;
                }
            }
        }
        //一直没找到，返回false
        return false;
    }
}
```

#### [153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

```
    public int findMin(int[] nums) {
        int len = nums.length;
        int left=0;
        int right=len-1;
        int mid;
        while(left<right){
            mid=(left+right)/2;
            if(nums[mid]>nums[right])
                left=mid+1;
            else 
                right=mid;
        }
        return nums[left];
    }
```

#### [154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

注意数组中可能存在重复的元素。

```
    public int findMin(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        while (low < high) {
            int pivot = low + (high - low) / 2;
            if (nums[pivot] < nums[high]) {
                high = pivot;
            } else if (nums[pivot] > nums[high]) {
                low = pivot + 1;
            } else {
                high -= 1;
            }
        }
        return nums[low];
    }
```

#### [4. 寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)







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

