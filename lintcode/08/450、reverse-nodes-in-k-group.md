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
450. K组翻转链表
中文English
给你一个链表以及一个k,将这个链表从头指针开始每k个翻转一下。
链表元素个数不是k的倍数，最后剩余的不用翻转。

样例
Example 1

Input:
list = 1->2->3->4->5->null
k = 2
Output:
2->1->4->3->5
Example 2

Input:
list = 1->2->3->4->5->null
k = 3
Output:
3->2->1->4->5
*/
public class Solution {
    /**
     * @param head: a ListNode
     * @param k: An integer
     * @return: a ListNode
     */
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode cur = dummy;
        while(true){
            cur = reverseKGroupHelper(cur,k);
            if(cur==null) break;
        }
        
        return dummy.next;
    }
    
    
    //翻转head开头k个，返回尾节点
    private ListNode reverseKGroupHelper(ListNode head,int k){
        ListNode nk = head;
        for(int i=0;i<k;++i){
            if(nk==null) return null;
            
            nk = nk.next;
        }
        
        if(nk==null) return null;
        ListNode n1 = head.next;
        ListNode nkplus = nk.next;
        
        ListNode prev = null;
        ListNode cur = n1;
        
        while(cur!=nkplus){
            ListNode temp = cur.next;
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        
        head.next = nk;
        n1.next = nkplus;
        
        return n1;
        
    }
}
```

