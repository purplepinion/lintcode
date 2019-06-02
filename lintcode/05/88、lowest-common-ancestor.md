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
88. 最近公共祖先
中文English
给定一棵二叉树，找到两个节点的最近公共父节点(LCA)。

最近公共祖先是两个节点的公共的祖先节点且具有最大深度。

样例
样例 1:

输入：{1},1,1
输出：1
解释：
 二叉树如下（只有一个节点）:
         1
 LCA(1,1) = 1
样例 2:

输入：{4,3,7,#,#,5,6},3,5
输出：4
解释：
 二叉树如下:

      4
     / \
    3   7
       / \
      5   6
			
 LCA(3, 5) = 4
注意事项
假设给出的两个节点都在树中存在

*/

public class Solution {

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        if(root==null||root==A||root==B) return root;
        
        //dvide and conquer
        TreeNode left = lowestCommonAncestor(root.left,A,B);
        TreeNode right = lowestCommonAncestor(root.right,A,B);
        
        //root为lca
        if(left!=null&&right!=null) return root;
        
        //LCA of A or B
        if(left!=null) return left;
        
        if(right!=null) return right;
        
        return null;
    }
}

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

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        ResultType result = helper(root,A,B);
        return result.lca;
    }
    
    private ResultType helper(TreeNode root,TreeNode A,TreeNode B){
        if(root==null) return new ResultType(false,false,null);
        if(root==A) return new ResultType(true,false,A);
        if(root==B) return new ResultType(false,true,B);
        
    
        //dvide and conquer
        ResultType left = helper(root.left,A,B);
        ResultType right = helper(root.right,A,B);
        
        if(left.hasA&&left.hasB) return left;
        if(right.hasA&&right.hasB) return right;
        
        boolean hasA = false,hasB = false;
        
        if(left.hasA||right.hasA){
            hasA = true;
        }
        if(left.hasB||right.hasB){
            hasB = true;
        }
        
        if(hasA&&hasB) return new ResultType(true,true,root);
        
        if(hasA) return new ResultType(true,false,A);
        
        if(hasB) return new ResultType(false,true,B);
        
        return new ResultType(false,false,null);
      /* 1
        # 2
         # 3 
          # 4
           # 5*/
    }
}
```

