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
68. Binary Tree Postorder Traversal
中文English
给出一棵二叉树，返回其节点值的后序遍历。

样例
样例 1:

输入：{1,2,3}
输出：[2,3,1]
解释： 
   1
  / \
 2   3
它将被序列化为{1,2,3}
后序遍历
样例 2:

输入：{1,#,2,3}
输出：[3,2,1]
解释： 
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
后序遍历
挑战
你能使用非递归实现么？

注意事项
首个数据为根节点，后面接着是其左儿子和右儿子节点值，"#"表示不存在该子节点。
节点数量不超过20

*/
public class Solution {
    /**
     * @param root: A Tree
     * @return: Postorder in ArrayList which contains node values.
     */
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        
        traverse(root,res);
        
        return res;
    }
    
     private void traverse(TreeNode root,List<Integer> list){
        if(root==null) return;
        
        traverse(root.left,list);
        traverse(root.right,list);
        list.add(root.val);
    }
}

public class Solution {
    /**
     * @param root: A Tree
     * @return: Postorder in ArrayList which contains node values.
     */
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
		//return 
        if(root==null) return res;
        
        //dvide
        List<Integer> left = postorderTraversal(root.left);
        List<Integer> right = postorderTraversal(root.right);
        
        //conquer(merge)
        res.addAll(left);
        res.addAll(right);
        res.add(root.val);
        
        return res;
    }
    
}
```

