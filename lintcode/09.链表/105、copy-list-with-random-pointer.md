```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
/*
105. 复制带随机指针的链表
中文English
给出一个链表，每个节点包含一个额外增加的随机指针可以指向链表中的任何节点或空的节点。

返回一个深拷贝的链表。 

挑战
可否使用O(1)的空间
*/

public class Solution {
   
    //用hashmap存储映射关系

    public RandomListNode copyRandomList(RandomListNode head) {
        if(head==null) return null;
        
        Map<RandomListNode,RandomListNode> map = new HashMap<RandomListNode,RandomListNode>();
        
        for(RandomListNode curNode=head;curNode!=null;curNode=curNode.next){
            RandomListNode newNode = new RandomListNode(curNode.label);
            newNode.next = curNode.next;
            map.put(curNode,newNode);
        }
        
        for(RandomListNode curNode=head;curNode!=null;curNode=curNode.next){
            map.get(curNode).random = map.get(curNode.random);
        }
        
        return map.get(head);
    }
}



public class Solution {

    public RandomListNode copyRandomList(RandomListNode head) {
        if(head==null) return null;
        copyNext(head);
        copyRandom(head);
        return double2single(head);
    }
    
    //1->2->3->null
    //1->1'->2->2'->3->3'->null
    private void copyNext(RandomListNode head){

        RandomListNode curNode = head;
        while(curNode!=null){
            RandomListNode newNode = new RandomListNode(curNode.label);
            newNode.next = curNode.next;
            curNode.next = newNode;
            curNode = curNode.next.next;
        }
    }
    
    private void copyRandom(RandomListNode head){
        
        RandomListNode curNode = head;
        while(curNode!=null){
            
            if(curNode.random==null){
                curNode.next.random = null;
            }else{
                curNode.next.random = curNode.random.next;
            }
            
            curNode=curNode.next.next;
        }
    }
    
    private RandomListNode double2single(RandomListNode head){

        RandomListNode ans = head.next;
        while(head!=null){
            RandomListNode temp = head.next;
            head.next = temp.next;
            head = head.next;
            if(temp.next!=null){
                temp.next=temp.next.next;
            }
        }
        
        return ans;
    }
}
```

