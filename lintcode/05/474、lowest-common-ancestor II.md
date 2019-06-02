```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public ParentTreeNode parent, left, right;
 * }
 */

/*
474. 最近公共祖先 II
中文English
给一棵二叉树和二叉树中的两个节点，找到这两个节点的最近公共祖先LCA。

两个节点的最近公共祖先，是指两个节点的所有父亲节点中（包括这两个节点），离这两个节点最近的公共的节点。

每个节点除了左右儿子指针以外，还包含一个父亲指针parent，指向自己的父亲。

样例
样例 1:

输入：{4,3,7,#,#,5,6},3,5
输出：4
解释：
     4
     / \
    3   7
       / \
      5   6
LCA(3, 5) = 4
样例 2:

输入：{4,3,7,#,#,5,6},5,6
输出：7
解释：
      4
     / \
    3   7
       / \
      5   6
LCA(5, 6) = 7
*/
public class Solution {

    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root, ParentTreeNode A, ParentTreeNode B) {
        ArrayList<ParentTreeNode> pathA = getPath(A);
        ArrayList<ParentTreeNode> pathB = getPath(B);
        
        ParentTreeNode lca = null;
        
        int index1 = pathA.size()-1;
        int index2 = pathB.size()-1;
        
        while(index1>=0&&index2>=0){
            if(pathA.get(index1)!=pathB.get(index2)) break;
            lca = pathA.get(index1);
            index1--;
            index2--;
        }
        
        return lca;
    }
    
    private ArrayList<ParentTreeNode> getPath(ParentTreeNode node){
        ArrayList<ParentTreeNode> path = new ArrayList<>();
        
        if(node==null) return path;
        
        while(node!=null){
            path.add(node);
            node = node.parent;
        }
        
        return path;
    }
}
```

