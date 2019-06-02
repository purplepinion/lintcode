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
class ResultType{
    public int sum;
    public int size;
    public ResultType(int sum,int size){
        this.sum = sum;
        this.size = size;
    }
}

public class Solution {
    /**
     * @param root: the root of binary tree
     * @return: the root of the maximum average of subtree
     */
    private TreeNode maxSubtree = null;
    private ResultType maxSubtreeAverage = null;

    public TreeNode findSubtree2(TreeNode root) {
        helper(root);
        return maxSubtree;
    }
    
    private ResultType helper(TreeNode root){
        if(root==null) return new ResultType(0,0);
        
        //dvide and conquer
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        
        ResultType result = new ResultType(
            left.sum + right.sum + root.val,
            left.size + right.size + 1
            );
            
        if(maxSubtree==null||maxSubtreeAverage.sum*result.size<maxSubtreeAverage.size*result.sum){
            maxSubtreeAverage = result;
            maxSubtree = root;
        }
        
        return result;
    }
}
```

