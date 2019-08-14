```java
104. 合并k个排序链表
中文English
合并k个排序链表，并且返回合并后的排序链表。尝试分析和描述其复杂度。

样例
样例 1:
	输入:   [2->4->null,null,-1->null]
	输出:  -1->2->4->null

样例 2:
	输入: [2->6->null,5->null,7->null]
	输出:  2->5->6->7->null
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /*O(nlogk)
    *用一个极小堆维护每个链表的头，从中取出并添加到返回的链表后*/
    public ListNode mergeKLists(List<ListNode> lists) {  
        if(lists==null || lists.size()==0){
            return null;
        }
        
        Queue<ListNode> heap = new PriorityQueue<ListNode>(lists.size(),listNodeComparator);
        
        for(int i=0;i<lists.size();i++){
            if(null!=lists.get(i)){
                heap.add(lists.get(i));
            }
        }
        
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        
        while(!heap.isEmpty()){
            ListNode temp = heap.poll();
            tail.next = temp;
            tail = temp;
            if(null!=temp.next){
                heap.add(temp.next);
            }
        }
        return dummy.next;
    }
    
    private Comparator<ListNode> listNodeComparator = new Comparator<ListNode>(){
        @Override
        public int compare(ListNode left,ListNode right){
            return left.val - right.val;
        }
    };
}

```

