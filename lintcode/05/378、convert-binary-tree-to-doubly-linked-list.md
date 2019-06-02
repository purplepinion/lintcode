```java
/**
 * Definition for Doubly-ListNode.
 * public class DoublyListNode {
 *     int val;
 *     DoublyListNode next, prev;
 *     DoublyListNode(int val) {
 *         this.val = val;
 *         this.next = this.prev = null;
 *     }
 * } * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
 /*
 378. 将二叉树转换成双链表
中文English
将一个二叉树按照中序遍历转换成双向链表。

样例
样例 1：

输入:
	    4
	   / \
	  2   5
	 / \
	1   3		

输出: 1<->2<->3<->4<->5
样例 2：

输入:
	    3
	   / \
	  4   1

输出:4<->3<->1
*/
class ResultType{
   DoublyListNode first;
   DoublyListNode last;
   
   public ResultType(DoublyListNode first,DoublyListNode last){
       this.first = first;
       this.last = last;
   }
}
public class Solution {
    /**
     * @param root: The root of tree
     * @return: the head of doubly list node
     */
    public DoublyListNode bstToDoublyList(TreeNode root) {
        ResultType result = helper(root);
        return result!=null?result.first:null;
    }
    
    private ResultType helper(TreeNode root){
        if(root==null) return null;
        
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        
        DoublyListNode newNode = new DoublyListNode(root.val);
        
        if(left!=null&&right!=null){
            left.last.next = newNode;
            newNode.next = right.first;
            return new ResultType(left.first,right.last);
        }
        
        if(left!=null){
            left.last.next = newNode;
            return new ResultType(left.first,newNode);
        }
        
        if(right!=null){
            newNode.next = right.first;
            return new ResultType(newNode,right.last);
        }
        return new ResultType(newNode,newNode);
    }
    
    
}
```

