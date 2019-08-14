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
95. 验证二叉查找树
中文English
给定一个二叉树，判断它是否是合法的二叉查找树(BST)

一棵BST定义为：

节点的左子树中的值要严格小于该节点的值。
节点的右子树中的值要严格大于该节点的值。
左右子树也必须是二叉查找树。
一个节点的树也是二叉查找树。
样例
样例 1:

输入：{-1}
输出：true
解释：
二叉树如下(仅有一个节点）:
	-1
这是二叉查找树。
样例 2:

输入：{2,1,4,#,#,3,5}
输出：true
解释：
	二叉树如下：
	  2
	 / \
	1   4
	   / \
	  3   5
这是二叉查找树。
*/
class ResultType{
    public boolean isBst;
    public long min;
    public long max;
    
    public ResultType(boolean isBst,long min,long max){
        this.isBst = isBst;
        this.min = min;
        this.max = max;
    }
}
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST(TreeNode root) {
        ResultType result = helper(root);
        return result.isBst;
    }
    
    private ResultType helper(TreeNode root){
        if(root==null) return new ResultType(true,Long.MAX_VALUE,Long.MIN_VALUE);
        
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        
        if(!left.isBst||!right.isBst){
            return new ResultType(false,0,0); 
        }
        
        if((left.isBst&&root.val<=left.max)||(right.isBst&&root.val>=right.min)){
            return new ResultType(false,0,0);
        }
        
        return new ResultType(true,Math.min(root.val,left.min),Math.max(root.val,right.max));
    }
}

public class Solution {

    public boolean isValidBST(TreeNode root) {
        return dvideConquuer(root,Long.MIN_VALUE,Long.MAX_VALUE);
    }
    
    private boolean dvideConquuer(TreeNode root,long min,long max){
        if(root==null) return true;
        
        if(root.val<=min || root.val>=max) return false;
        
        return dvideConquuer(root.left,min,root.val)&&dvideConquuer(root.right,root.val,max);
    }
    
    
}
```

