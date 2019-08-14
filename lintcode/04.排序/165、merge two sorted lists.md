```java

/*
165. 合并两个排序链表
中文English
将两个排序链表合并为一个新的排序链表

样例
样例 1:
	输入: list1 = null, list2 = 0->3->3->null
	输出: 0->3->3->null


样例2:
	输入:  list1 =  1->3->8->11->15->null, list2 = 2->null
	输出: 1->2->3->8->11->15->null
*/	
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

public class Solution {
    /**
     * @param l1: ListNode l1 is the head of the linked list
     * @param l2: ListNode l2 is the head of the linked list
     * @return: ListNode head of linked list
     */
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        final ListNode head = new ListNode(-1);
        ListNode last = head;
        
        while(l1!=null&&l2!=null){
            if(l1.val<l2.val){
                last.next=l1;
                l1=l1.next;
            }else{
                last.next=l2;
                l2=l2.next;
            }
            
            last = last.next;
        }
        
        if(l1!=null){
            last.next = l1;
        }
        else if(l2!=null){
            last.next = l2;
        }
        
        return head.next;
    }
}
```

