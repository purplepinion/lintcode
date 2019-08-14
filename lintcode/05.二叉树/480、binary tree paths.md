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
480. 二叉树的所有路径
中文English
给一棵二叉树，找出从根节点到叶子节点的所有路径。

样例
样例 1:

输入：{1,2,3,#,5}
输出：["1->2->5","1->3"]
解释：
   1
 /   \
2     3
 \
  5
样例 2:

输入：{1,2}
输出：["1->2"]
解释：
   1
 /   
2     */
public class Solution {
    /**
     * @param root: the root of the binary tree
     * @return: all root-to-leaf paths
     */
     
    //1.递归定义：输入root 找到root2leaf的path 并返回
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> paths = new ArrayList<String>();
        
        //3.递归出口
        if(root==null) return paths;
        if(root.left==null&&root.right==null){
            paths.add(""+root.val);
            return paths;
        }
        
        //2.divide and conquer (merge)
        List<String> leftPaths = binaryTreePaths(root.left);
        List<String> rightPaths = binaryTreePaths(root.right);
        
        for(String path:leftPaths){
            paths.add(root.val + "->" + path);
        } 
        for(String path:rightPaths){
            paths.add(root.val + "->" + path);
        } 
        
        return paths;
    }
}
```

