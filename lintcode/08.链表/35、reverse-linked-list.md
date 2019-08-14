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
35. 翻转链表
中文English
翻转一个链表

样例
样例 1:

输入: 1->2->3->null
输出: 3->2->1->null
样例 2:

输入: 1->2->3->4->null
输出: 4->3->2->1->null
挑战
在原地一次翻转完成
*/
public class Solution {
    /**
     * @param head: n
     * @return: The new head of reversed linked list.
     */
    public ListNode reverse(ListNode head) {

        if(head==null||head.next==null) return head;
        
        ListNode prev = null;
        ListNode cur = head;
        while(cur!=null){
            ListNode  temp = cur.next;
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        
        return prev;
    }
}
```

