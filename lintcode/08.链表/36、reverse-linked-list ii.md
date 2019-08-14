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
36. 翻转链表 II
中文English
翻转链表中第m个节点到第n个节点的部分

样例
例1:

输入: 1->2->3->4->5->NULL, m = 2 and n = 4, 
输出: 1->4->3->2->5->NULL.
例2:

输入: 1->2->3->4->NULL, m = 2 and n = 3, 
输出: 1->3->2->4->NULL.
挑战
Reverse it in-place and in one-pass

注意事项
m，n满足1 ≤ m ≤ n ≤ 链表长度
*/
public class Solution {
    /**
     * @param head: ListNode head is the head of the linked list 
     * @param m: An integer
     * @param n: An integer
     * @return: The head of the reversed ListNode
     */
    
    //head->n1->[n2->n3->n4]->n5->null
    //=>
    //head->n1->[n4->n3->n2]->n5->null
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        //find nodem
        ListNode nodem = dummy;
        for(int i=1;i<m;++i){
            if(nodem==null) return null;
            nodem = nodem.next;
        }
        ListNode prev = nodem;
        nodem = nodem.next;
        
        //reverse m - n
        ListNode noden = nodem;
        ListNode cur = noden.next;
        for(int i=m;i<n;++i){
            if(cur==null) return null;
            ListNode temp = cur.next;
            cur.next = noden;
            noden = cur;
            cur = temp;
        }
        
        nodem.next = cur;
        prev.next = noden;
        
        return dummy.next;
    }
}
```

