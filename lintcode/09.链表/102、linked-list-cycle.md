~~~java
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
102. 带环链表
中文English
给定一个链表，判断它是否有环。

样例
```
样例 1:
	输入: 21->10->4->5,  then tail connects to node index 1(value 10).
	输出: true
	
样例 2:
	输入: 21->10->4->5->null
	输出: false

```
挑战
不要使用额外的空间
*/
public class Solution {
    //快慢指针
    public boolean hasCycle(ListNode head) {
        if(head==null) return false;
        
        ListNode fast = head;
        ListNode slow = head;
        
        while(fast!=null&&fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            
            if(fast==slow) return true;
        }
        
        return false;
    }
}
~~~

