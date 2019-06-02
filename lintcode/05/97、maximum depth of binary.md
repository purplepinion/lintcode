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
97. 二叉树的最大深度
中文English
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的距离。

样例
样例 1:

输入: tree = {}
输出: 0	
样例解释: 空树的深度是0。
样例 2:

输入: tree = {1,2,3,#,#,4,5}
输出: 3
样例解释: 树表示如下，深度是3
   1
  / \                
 2   3                
    / \                
   4   5
它将被序列化为{1,2,3,#,#,4,5}
*/
/*
public class Solution {
     
    private int depth;
    
    public int maxDepth(TreeNode root) {
        depth = 0;
        helper(root,1);
        return depth;
    }
    
    private void helper(TreeNode root,int curDepth){
        if(root==null) return ;
        
        if(curDepth>depth){
            depth = curDepth;
        }
        
        helper(root.left,curDepth+1);
        helper(root.right,curDepth+1);
    }
}*/
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: An integer
     */
    public int maxDepth(TreeNode root) {
        
        if(root==null) return 0;
        
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        
        return (left>right?left:right)+1;
    }
}

```

