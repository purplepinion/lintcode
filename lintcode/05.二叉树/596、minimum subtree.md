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
596. 最小子树
中文English
给一棵二叉树, 找到和为最小的子树, 返回其根节点。

样例
样例 1:

输入:
{1,-5,2,1,2,-4,-5}
输出:1
说明
这棵树如下所示：
     1
   /   \
 -5     2
 / \   /  \
1   2 -4  -5 
整颗树的和是最小的，所以返回根节点1.
样例 2:

输入:
{1}
输出:1
说明:
这棵树如下所示：
   1
这棵树只有整体这一个子树，所以返回1.
注意事项
LintCode会打印根节点为你返回节点的子树。保证只有一棵和最小的子树并且给出的二叉树不是一棵空树。
*/

public class Solution {//travere + divide conquer
 
    private TreeNode subtree = null;
    private int minSum = Integer.MAX_VALUE;
    
    public TreeNode findSubtree(TreeNode root) {
        helper(root);
        return subtree;
    }
    
    private int helper(TreeNode root){
        if(root==null) return 0;
        
        //dvide and conquer
        int sum = helper(root.left) + helper(root.right) + root.val;
        
        //Compare
        if(sum<minSum){
            minSum = sum;
            subtree = root;
        }
        
        return sum;
    }
    
}

class ResultType{
    public TreeNode subtree;
    public int sum,minSum;
    
    public ResultType(TreeNode subtree,int sum,int minSum){
        this.subtree = subtree;
        this.sum = sum;
        this.minSum = minSum;
    }
}

//travere + divide conquer
public class Solution {
    /**
     * @param root: the root of binary tree
     * @return: the root of the minimum subtree
     */

    public TreeNode findSubtree(TreeNode root) {
        ResultType res = helper(root);
        return res.subtree;
    }
    
    private ResultType helper(TreeNode root){
        
        if(root==null) return new ResultType(null,0,Integer.MAX_VALUE);
        
        //2.dvide and conquer
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        
        ResultType result = new ResultType(
            root,
            left.sum+right.sum+root.val,
            left.sum+right.sum+root.val
            );
            
        if(left.minSum<=result.minSum){
            result.minSum = left.minSum;
            result.subtree = left.subtree;
        }
        
        if(right.minSum<=result.minSum){
            result.minSum = right.minSum;
            result.subtree = right.subtree;
        }
        
        return result;
    }
    
}
    
```

