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
98. 链表排序
中文English
在 O(n log n) 时间复杂度和常数级的空间复杂度下给链表排序。

样例
Example 1:

Input:  1->3->2->null
Output:  1->2->3->null
Example 2:

Input: 1->7->2->6->null
Output: 1->2->6->7->null	
挑战
分别用归并排序和快速排序做一遍。
*/
public class Solution {
    
    //merge sort
    public ListNode sortList(ListNode head) {
        if(head==null||head.next==null) return head;
        
        ListNode mid = getMid(head);
        //notice mid.next
        ListNode right = sortList(mid.next);
        mid.next = null;
        ListNode left = sortList(head);
        
        return merge(left,right);
    }
    
    //fast and  slow to find mid 
    private ListNode getMid(ListNode head){
        ListNode fast = head.next;
        ListNode slow = head;
        
        while(fast!=null&&fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        return slow;
    }
    
    private ListNode merge(ListNode left,ListNode right){
        
        ListNode dummy = new ListNode(0);
        ListNode curNode = dummy;
        while(left!=null&&right!=null){
            if(left.val<right.val){
                curNode.next = left;
                left = left.next;
            }else{
                curNode.next = right;
                right = right.next;
            }
            curNode = curNode.next;
        }
        
        if(left!=null){
            curNode.next = left;
        }else if(right!=null){
            curNode.next = right;
        }
        
        return dummy.next;
    }
    
    
    
}
```

