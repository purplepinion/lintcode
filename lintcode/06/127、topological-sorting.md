```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */
/*
127. 拓扑排序
中文English
给定一个有向图，图节点的拓扑排序定义如下:

对于图中的每一条有向边 A -> B , 在拓扑排序中A一定在B之前.
拓扑排序中的第一个节点可以是图中的任何一个没有其他节点指向它的节点.
针对给定的有向图找到任意一种拓扑排序的顺序.

样例
例如以下的图:

picture

拓扑排序可以为:

[0, 1, 2, 3, 4, 5]
[0, 2, 3, 1, 5, 4]
挑战
能否分别用BFS和DFS完成？

说明
有关图的表示详情请看这里

注意事项
你可以假设图中至少存在一种拓扑排序

*/
public class Solution {
    /*
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        ArrayList<DirectedGraphNode> order = new ArrayList<>();
        
        if(graph==null){
            return order;
        }
        //1.计算所有顶点入度
        Map<DirectedGraphNode,Integer> indegree = indegree(graph);
        
        //2.获得入度为0的顶点
        ArrayList<DirectedGraphNode> startNodes = getStartNodes(indegree,graph);
        
        //3.bfs 获得一条路径
        order = bfs(indegree,startNodes);
        
        if(order.size()==graph.size()){
            return order;
        }
        
        return null;
    }
    
    /*
     * @param graph:  graph
     * @return: indegree
     */
    private Map<DirectedGraphNode,Integer> indegree(ArrayList<DirectedGraphNode> graph){
        Map<DirectedGraphNode,Integer> indegree = new HashMap<DirectedGraphNode,Integer>();
        
        
        for(DirectedGraphNode node:graph){
            indegree.put(node,0);
        }
        //求入度
        for(DirectedGraphNode curNode:graph){
            for(DirectedGraphNode neighbor:curNode.neighbors){
                indegree.put(neighbor,indegree.get(neighbor)+1);
            }
        }
        return indegree;
    }
    /*
     * @param graph:  indegree graph
     * @return: startNodes
     */
    private ArrayList<DirectedGraphNode> getStartNodes(
        Map<DirectedGraphNode,Integer> indegree,
        ArrayList<DirectedGraphNode> graph
        )
    {
        ArrayList<DirectedGraphNode> startNodes = new ArrayList<DirectedGraphNode>();
        
        for(DirectedGraphNode node:graph){
            if(indegree.get(node)==0){
                startNodes.add(node);
            }
        }
        return startNodes;
    }
    
    /*
     * @param graph:  indegree startNodes
     * @return: order
     */
    private ArrayList<DirectedGraphNode> bfs(
        Map<DirectedGraphNode,Integer> indegree,
        ArrayList<DirectedGraphNode> startNodes
        )
    {
        ArrayList<DirectedGraphNode> order = new ArrayList<>();
        Queue<DirectedGraphNode> queue = new LinkedList<DirectedGraphNode>();
        
        for(DirectedGraphNode startNode:startNodes){
            order.add(startNode);
            queue.offer(startNode);
        }
        
        while(!queue.isEmpty()){
            DirectedGraphNode curNode = queue.poll();
            
            for(DirectedGraphNode neighbor:curNode.neighbors){
                indegree.put(neighbor,indegree.get(neighbor)-1);
                if(indegree.get(neighbor)==0){
                    order.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }
        
        return order;
    }
}
```

