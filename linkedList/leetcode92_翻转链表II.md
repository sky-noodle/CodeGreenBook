# CodeGreenBook

### Leetcode

#### [92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。

说明:
1 ≤ m ≤ n ≤ 链表长度。

示例:

输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-linked-list-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 思路：

```
1.首先移动pre节点到m的前一位置；
2.从m到n翻转链表；
3.链接翻转后的局部链表，开始翻转的节点（2）指向当前节点（5），pre（1）指向局部的前节点(4);
```

### 算法设计技巧：

1.考虑m可能是0，因此引入dummy节点；

2.翻转链表前存储开始翻转的节点，用于链接翻转后的链表；

3.翻转后cur节点指向翻转后的的下一节点(5),局部pre节点存储的是cur的前一节点；



### 注意点：



代码：

```
package linkedList;

public class reverseBetween {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if(head==null || m>=n){
            return head;
        }
        ListNode dumpy = new ListNode(0);
        dumpy.next = head;
        ListNode pre = dumpy;
        for(int i=0;i<m-1;i++){
            if(pre==null){
                return null;
            }
            pre = pre.next;
        }
        ListNode mList = pre.next;
        ListNode cur = mList.next;
        ListNode nList = mList;
        for(int i=m;i<n;i++){
            if(cur==null){
                return null;
            }
            ListNode next = cur.next;
            cur.next = nList;
            nList = cur;
            cur=next;
        }
        mList.next = cur;
        pre.next = nList;
        return dumpy.next;
    }
}


```







