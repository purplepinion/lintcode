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
69. 二叉树的层次遍历
中文English
给出一棵二叉树，返回其节点值的层次遍历（逐层从左往右访问）

样例
样例 1:

输入：{1,2,3}
输出：[[1],[2,3]]
解释：
   1
  / \
 2   3
它将被序列化为{1,2,3}
层次遍历
样例 2:

输入：{1,#,2,3}
输出：[[1],[2],[3]]
解释：
1
*/
public class Solution {
    /**
     * @param root: A Tree
     * @return: Level order a list of lists of integer
     */
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> results = new ArrayList<>();
        
        if(root==null) return results;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while(!queue.isEmpty()){
            List<Integer> curLevel = new ArrayList<Integer>();
            
            int size = queue.size();
            for(int i=0;i<size;++i){
                TreeNode node = queue.poll();
                curLevel.add(node.val);
                
                if(node.left!=null){
                    queue.offer(node.left);
                }
                
                if(node.right!=null){
                    queue.offer(node.right);
                }
            }
            //no deep copy
            results.add(curLevel);
        }
        
        return results;
    }
}
```

