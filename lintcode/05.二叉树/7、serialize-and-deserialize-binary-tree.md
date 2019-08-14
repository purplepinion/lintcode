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

7. 二叉树的序列化和反序列化
中文English
设计一个算法，并编写代码来序列化和反序列化二叉树。将树写入一个文件被称为“序列化”，读取文件后重建同样的二叉树被称为“反序列化”。

如何反序列化或序列化二叉树是没有限制的，你只需要确保可以将二叉树序列化为一个字符串，并且可以将字符串反序列化为原来的树结构。

样例
样例 1：

输入：{3,9,20,#,#,15,7}
输出：{3,9,20,#,#,15,7}
解释：
二叉树 {3,9,20,#,#,15,7}，表示如下的树结构：
	  3
	 / \
	9  20
	  /  \
	 15   7
它将被序列化为 {3,9,20,#,#,15,7}
样例 2：

输入：{1,2,3}
输出：{1,2,3}
解释：
二叉树 {1,2,3}，表示如下的树结构：
   1
  / \
 2   3
它将被序列化为 {1,2,3}
我们的数据是进行 BFS 遍历得到的。当你测试结果 Wrong Answer 时，你可以作为输入调试你的代码。

你可以采用其他的方法进行序列化和反序列化。

注意事项
对二进制树进行反序列化或序列化的方式没有限制，LintCode 将您的 serialize 输出作为 deserialize 的输入，它不会检查序列化的结果。*/

public class Solution {

    public String serialize(TreeNode root) {
        
        if(root==null) return "{}";
        
        StringBuilder sb = new StringBuilder();
        
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        
        queue.offer(root);
        sb.append("{");
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            if(node==null) {
                sb.append("#,");
                continue;
            }
            else {
                sb.append(node.val+",");
            }
            
            queue.offer(node.left);
            queue.offer(node.right);    
        }
        sb.delete(sb.length()-1,sb.length());
        sb.append("}");
        
        return sb.toString();
        /*
        if (root == null) {
            return "{}";
        }

        ArrayList<TreeNode> queue = new ArrayList<TreeNode>();
        queue.add(root);

        for (int i = 0; i < queue.size(); i++) {
            TreeNode node = queue.get(i);
            if (node == null) {
                continue;
            }
            queue.add(node.left);
            queue.add(node.right);
        }

        while (queue.get(queue.size() - 1) == null) {
            queue.remove(queue.size() - 1);
        }

        StringBuilder sb = new StringBuilder();
        sb.append("{");
        sb.append(queue.get(0).val);
        for (int i = 1; i < queue.size(); i++) {
            if (queue.get(i) == null) {
                sb.append(",#");
            } else {
                sb.append(",");
                sb.append(queue.get(i).val);
            }
        }
        sb.append("}");
        return sb.toString();*/
    }


    public TreeNode deserialize(String data) {
        
        StringBuilder sb = new StringBuilder(data);
        sb.delete(0,1);
        sb.delete(sb.length()-1,sb.length());
        String[] strs = sb.toString().split(",");
        
        if(strs.length==0||data.equals("{}")) return null;
        
        TreeNode root = new TreeNode(Integer.parseInt(strs[0]));
        int i = 1;
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        
        while(!queue.isEmpty()&&i<strs.length){
            TreeNode node = queue.poll();
            
            if(strs[i].equals("#")){
                node.left = null;
                i++;
            }else{
                node.left = new TreeNode(Integer.parseInt(strs[i]));
                i++;
                queue.offer(node.left);
            }
            
            if(strs[i].equals("#")){
                node.right = null;
                i++;
            }else{
                node.right = new TreeNode(Integer.parseInt(strs[i]));
                i++;
                queue.offer(node.right);
            }
        }
        return root;
        /*
        if (data.equals("{}")) {
            return null;
        }
        String[] vals = data.substring(1, data.length() - 1).split(",");
        ArrayList<TreeNode> queue = new ArrayList<TreeNode>();
        TreeNode root = new TreeNode(Integer.parseInt(vals[0]));
        queue.add(root);
        int index = 0;
        boolean isLeftChild = true;
        for (int i = 1; i < vals.length; i++) {
            if (!vals[i].equals("#")) {
                TreeNode node = new TreeNode(Integer.parseInt(vals[i]));
                if (isLeftChild) {
                    queue.get(index).left = node;
                } else {
                    queue.get(index).right = node;
                }
                queue.add(node);
            }
            if (!isLeftChild) {
                index++;
            }
            isLeftChild = !isLeftChild;
        }
        return root;*/
    }
}
```

