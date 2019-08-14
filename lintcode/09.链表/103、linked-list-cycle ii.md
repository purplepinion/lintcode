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

103. 带环链表 II
中文English
给定一个链表，如果链表中存在环，则返回到链表中环的起始节点，如果没有环，返回null。

样例
样例 1:

输入：null,no cycle
输出：no cycle
解释：
链表为空，所以没有环存在。
样例 2:

输入：-21->10->4->5，tail connects to node index 1
输出：10
解释：
最后一个节点5指向下标为1的节点，也就是10，所以环的入口为10。
挑战
不使用额外的空间
*/
public class Solution {
    //快慢指针判断有环没
    //若有环则slow走了m+t fast走了m+kn+t=2*(m+t)  m=(k-1)n + n-t
    //让fast=head 则fast和slow相遇时为m 就是入口
    public ListNode detectCycle(ListNode head) {
        
        if(head==null) return null;
        
        ListNode fast = head;
        ListNode slow = head;
        
        while(fast!=null&&fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            
            if(fast==slow) break;
        }
        
        //无环
        if(fast==null||fast.next==null){
            return null;
        }
        
        //有环
        slow = head;
        while(slow!=fast){
            slow = slow.next;
            fast = fast.next;
        }
        
        return slow;
    }
}
```



