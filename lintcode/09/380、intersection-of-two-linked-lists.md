```java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
/*
380. 两个链表的交叉
中文English
请写一个程序，找到两个单链表最开始的交叉节点。

样例
样例 1：

输入：
	A:          a1 → a2
	                   ↘
	                     c1 → c2 → c3
	                   ↗            
	B:     b1 → b2 → b3
输出：c1
解释：在节点 c1 开始交叉。
样例 2:

输入:
Intersected at 6
1->2->3->4->5->6->7->8->9->10->11->12->13->null
6->7->8->9->10->11->12->13->null
输出: Intersected at 6
解释：begin to intersect at node 6.
挑战
需满足 O(n) 时间复杂度，且仅用 O(1) 内存。

注意事项
如果两个链表没有交叉，返回null。
在返回结果后，两个链表仍须保持原有的结构。
可假定整个链表结构中没有循环。
*/
public class Solution {
    
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        
        if(headA==null||headB==null) return null;
        
        ListNode rearA = headA;
        while(rearA!=null&&rearA.next!=null){
            rearA = rearA.next;
        }
        
        ListNode rearB = headB;
        while(rearB!=null&&rearB.next!=null){
            rearB = rearB.next;
        }
        
        //没有交点
        if(rearA!=rearB) return null;
        
        //有交点
        //转化为有环链表求环入口
        rearB.next = headA;
        
        ListNode fast = headB;
        ListNode slow = headB;
        
        while(fast!=null&&fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow==fast) break;
        }
        
        //if(fast=null||fast.next==null) return null;
        
        fast = headB;
        while(fast!=slow){
            fast = fast.next;
            slow = slow.next;
        }
        
        return fast;
    }
}
```

