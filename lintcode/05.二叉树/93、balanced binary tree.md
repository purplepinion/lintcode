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
public class Solution {

    private int NOT_BALANCED = -1;
    public boolean isBalanced(TreeNode root) {
        
        return maxDepth(root) != NOT_BALANCED;
    }
    
    private int maxDepth(TreeNode root){
        if(root==null) return 0;
        
        //divide and conquer
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        
        if(Math.abs(left-right)>1||left==NOT_BALANCED||right==NOT_BALANCED){
            return NOT_BALANCED;
        }
        
        return Math.max(left,right) + 1;
    }
}
*/
class ResultType{
    public boolean isBalanced;
    public int depth;
    
    public ResultType(boolean isBalanced,int depth){
        this.isBalanced = isBalanced;
        this.depth = depth;
    }
}
public class Solution {

    public boolean isBalanced(TreeNode root) {
        ResultType result = helper(root);
        return result.isBalanced;
    }
    
    private ResultType helper(TreeNode root){
        if(root==null) return new ResultType(true,0);
        
        //divide + conquer
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        
        if(!left.isBalanced||!right.isBalanced||Math.abs(left.depth-right.depth)>1){
            return new ResultType(false,-1);
        }
        
        return new ResultType(true,Math.max(left.depth,right.depth)+1);
    }
}
```

​	