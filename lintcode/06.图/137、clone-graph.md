```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */

/*
137. 克隆图
中文English
克隆一张无向图. 无向图的每个节点包含一个 label 和一个列表 neighbors. 保证每个节点的 label 互不相同.

你的程序需要返回一个经过深度拷贝的新图. 新图和原图具有同样的结构, 并且对新图的任何改动不会对原图造成任何影响.

样例
样例1

输入:
{1,2,4#2,1,4#4,1,2}
输出: 
{1,2,4#2,1,4#4,1,2}
解释:
1------2  
 \     |  
  \    |  
   \   |  
    \  |  
      4   
说明
关于无向图的表示: http://www.lintcode.com/help/graph/

注意事项
你需要返回与给定节点具有相同 label 的那个节点.

*/
public class Solution {
    /*
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        //1.node ->nodes
        //2.copy nodes
        //3.copy edges
        
        if(node==null) return node;
        
        //find all veterx
        ArrayList<UndirectedGraphNode> nodes = gerNodes(node);
        
        //copy nodes
        Map<UndirectedGraphNode,UndirectedGraphNode> mapping = new HashMap<>();
        for(UndirectedGraphNode n:nodes){
            mapping.put(n,new UndirectedGraphNode(n.label));
        }
        
        //copy edges
        
        for(UndirectedGraphNode n:nodes){
            UndirectedGraphNode newNode = mapping.get(n);
            for(UndirectedGraphNode neighbor:n.neighbors){
                UndirectedGraphNode newNeighbor = mapping.get(neighbor);
                newNode.neighbors.add(newNeighbor);
            }
        }
        
        return mapping.get(node);
    }
    
    
    private ArrayList<UndirectedGraphNode> gerNodes(UndirectedGraphNode node){
        Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        Set<UndirectedGraphNode> hash = new HashSet<UndirectedGraphNode>();
        
        queue.offer(node);
        hash.add(node);
        
        while(!queue.isEmpty()){
            UndirectedGraphNode curNode = queue.poll();
            for(UndirectedGraphNode neighbor:curNode.neighbors){
                if(hash.contains(neighbor)){
                    continue;
                }
            
                hash.add(neighbor);
                queue.offer(neighbor);
            }
        }
        
        return new ArrayList<UndirectedGraphNode>(hash);
    }
}
```

