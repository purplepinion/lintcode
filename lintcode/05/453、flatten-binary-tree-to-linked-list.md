```java
/**
 * Definition of TreeNode:
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
453. 将二叉树拆成链表
中文English
将一棵二叉树按照前序遍历拆解成为一个 假链表。所谓的假链表是说，用二叉树的 right 指针，来表示链表中的 next 指针。

样例
样例 1：

输入：{1,2,5,3,4,#,6}
输出：{1,#,2,#,3,#,4,#,5,#,6}
解释：
     1
    / \
   2   5
  / \   \
 3   4   6
 
1
\
 2
  \
   3
    \
     4
      \
       5
        \
         6
样例 2：

输入：{1}
输出：{1}
解释：
         1
         1
挑战
不使用额外的空间耗费。

注意事项
不要忘记将左儿子标记为 null，否则你可能会得到空间溢出或是时间溢出。*/
/*
public class Solution {

     
    private TreeNode lastNode = null;
    
    public void flatten(TreeNode root) {
        if(root==null) return;
        
        if(lastNode!=null){
            lastNode.left = null;
            lastNode.right = root;
        }
        
        lastNode = root;
        TreeNode right = root.right;
        flatten(root.left);
        flatten(right);
    }
}*/
public class Solution {
    
    public void flatten(TreeNode root) {
        helper(root);
    }
    
    private TreeNode helper(TreeNode root){
        if(root==null) return null;
        
        TreeNode leftLast = helper(root.left);
        TreeNode rightLast = helper(root.right);
        
        if(leftLast!=null) {
            leftLast.right = root.right;
            root.right = root.left;
            root.left = null;
        }   
        
        if(rightLast!=null){
            return rightLast;
        }
        
        if(leftLast!=null){
            return leftLast;
        }
        
        return root;
    }
}

```

