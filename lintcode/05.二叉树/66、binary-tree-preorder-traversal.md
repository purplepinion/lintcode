```java
/*
66. 二叉树的前序遍历
中文English
给出一棵二叉树，返回其节点值的前序遍历。

样例
样例 1:

输入：{1,2,3}
输出：[1,2,3]
解释：
   1
  / \
 2   3
它将被序列化为{1,2,3}
前序遍历
样例 2:

输入：{1,#,2,3}
输出：[1,2,3]
解释：
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
前序遍历
挑战
你能使用非递归实现么？

注意事项
首个数据为根节点，后面接着是其左儿子和右儿子节点值，"#"表示不存在该子节点。
节点数量不超过20
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

public class Solution {
    /**
     * @param root: A Tree
     * @return: Preorder in ArrayList which contains node values.
     */
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        //4.递归调用
        traverse(root,res);
        
        return res;
    }
    //递归三要素：
    //1.递归定义：给定节点获得前序遍历放入list集合
    private void traverse(TreeNode root,List<Integer> list){
        //3.递归出口：当节点为空返回
        if(root==null) return;
        
        //2.递归分解：将根的val加入list，加入左子树遍历，加入右子树的遍历
        list.add(root.val);
        traverse(root.left,list);
        traverse(root.right,list);
    }
}

public class Solution {
    /**
     * @param root: A Tree
     * @return: Preorder in ArrayList which contains node values.
     */
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
		
        if(root==null) return res;
        
        List<Integer> left = preorderTraversal(root.left);
        List<Integer> right = preorderTraversal(root.right);
        
        res.add(root.val);
        res.addAll(left);
        res.addAll(right);
        
        return res;
    }
}
```

