# CodeGreenBook

### Leetcode 

#### [82. 删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:

输入: 1->2->3->3->4->4->5 
输出: 1->2->5
示例 2:        

输入: 1->1->1->2->3
输出: 2->3

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路：

```
1.头节点可能被删除，引入dummy node，指向头节点；
2.因为是把所有重复的节点包括自己都删除，因此cur指向的是不重复的节点，cur.next 和cur.next.next去判断重复删除；
```

### 算法设计技巧：



### 注意点：



代码：

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode cur = dummy;
        while (cur.next!=null&&cur.next.next!=null){
            if(cur.next.val==cur.next.next.val){
            int tmpVal = cur.next.val;
            while (cur.next!=null&&cur.next.val==tmpVal){
                cur.next = cur.next.next;
            }
            }else{
                cur = cur.next;
            }
        }
        return dummy.next;
    }
}
```







