

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
578. 最近公共祖先 III
中文English
给一棵二叉树和二叉树中的两个节点，找到这两个节点的最近公共祖先LCA。

两个节点的最近公共祖先，是指两个节点的所有父亲节点中（包括这两个节点），离这两个节点最近的公共的节点。

返回 null 如果两个节点在这棵树上不存在最近公共祖先的话。

样例
样例1

输入: 
{4, 3, 7, #, #, 5, 6}
3 5
5 6
6 7 
5 8
输出: 
4
7
7
null
解释:
  4
 / \
3   7
   / \
  5   6

LCA(3, 5) = 4
LCA(5, 6) = 7
LCA(6, 7) = 7
LCA(5, 8) = null

样例2

输入:
{1}
1 1
输出: 
1
说明：
这棵树只有一个值为1的节点
注意事项
这两个节点未必都在这棵树上出现。

*/

class ResultType{
    boolean hasA;
    boolean hasB;
    TreeNode lca;
    
    public ResultType(boolean hasA,boolean hasB,TreeNode lca){
        this.hasA = hasA;
        this.hasB = hasB;
        this.lca = lca;
    }
}

public class Solution {

    public TreeNode lowestCommonAncestor3(TreeNode root, TreeNode A, TreeNode B) {
        ResultType result = helper(root,A,B);
        return (result.hasA&&result.hasB)?result.lca:null;
    }
    
    private ResultType helper(TreeNode root,TreeNode A,TreeNode B){
        if(root==null) return new ResultType(false,false,null);
        
    
        //dvide and conquer
        ResultType left = helper(root.left,A,B);
        ResultType right = helper(root.right,A,B);
        
        if(left.hasA&&left.hasB) return left;
        if(right.hasA&&right.hasB) return right;
        
        boolean hasA = false,hasB = false;
        
        if(left.hasA||right.hasA||root==A){
            hasA = true;
        }
        if(left.hasB||right.hasB||root==B){
            hasB = true;
        }
        
        if(hasA&&hasB) return new ResultType(true,true,root);
        
        if(hasA) return new ResultType(true,false,A);
        
        if(hasB) return new ResultType(false,true,B);
        
        return new ResultType(false,false,null);
      /* 1
        # 2
      */
        //1，-1
    }
}
```

