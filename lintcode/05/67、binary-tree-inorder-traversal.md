```java
/*
67. 二叉树的中序遍历
中文English
给出一棵二叉树,返回其中序遍历

样例
样例 1:

输入：{1,2,3}
输出：[2,1,3]
解释：
   1
  / \
 2   3
它将被序列化为{1,2,3}
中序遍历
样例 2:

输入：{1,#,2,3}
输出：[1,3,2]
解释：
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
中序遍历
挑战
你能使用非递归算法来实现么?
*/
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
    /**
     * @param root: A Tree
     * @return: Inorder in ArrayList which contains node values.
     */

public class Solution {

    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        
        traverse(root,res);
        
        return res;
    }
    
    private void traverse(TreeNode root,List<Integer> list){
        if(root==null) return;
        
        traverse(root.left,list);
        list.add(root.val);
        traverse(root.right,list);
    }
}

public class Solution {

    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
		//return 
        if(root==null) return res;
        
        //dvide
        List<Integer> left = inorderTraversal(root.left);
        List<Integer> right = inorderTraversal(root.right);
        
        //conquer(merge)
        res.addAll(left);
        res.add(root.val);
        res.addAll(right);
        
        return res;
    }
    

}

```

