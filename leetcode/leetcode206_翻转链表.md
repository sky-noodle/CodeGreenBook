# CodeGreenBook

### Leetcode

#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

反转一个单链表。

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

### 思路：

```
使用next指针指向cur之后节点，防止断链；
示例：
1.
1->2->3->null
pre = null；
cur = 1;
next = 2;
首先断1-2，1.next=pre;
pre向后移 pre=cur；
cur向后移 cur=next；
2.第二次迭代，null<-1 2->3->null;
当前pre=1，cur=2，next=3；
同步第一步操作即可
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
    public ListNode reverseList(ListNode head) {
        if(head==null){
            return null;
        }
        ListNode cur = head;
        ListNode pre = null;
        while (cur!=null){
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}

```







