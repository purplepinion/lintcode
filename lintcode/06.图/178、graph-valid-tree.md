```java
/*
178. 图是否是树
中文English
给出 n 个节点，标号分别从 0 到 n - 1 并且给出一个 无向 边的列表 (给出每条边的两个顶点), 写一个函数去判断这张｀无向｀图是否是一棵树

样例
样例 1:

输入: n = 5 edges = [[0, 1], [0, 2], [0, 3], [1, 4]]
输出: true.
样例 2:

输入: n = 5 edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]
输出: false.
注意事项
你可以假设我们不会给出重复的边在边的列表当中. 无向边　[0, 1] 和 [1, 0]　是同一条边， 因此他们不会同时出现在我们给你的边的列表当中。
*/
public class Solution {
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        //tree n vertx,n-1 eage
        //vi to vj isOK
        
        if(n==0) return false;
        if(edges.length!=n-1) return false;
        
        Map<Integer,Set<Integer>> graph = initializeGraph(n,edges);
        
        //bfs
        Queue<Integer> queue = new LinkedList<Integer>();
        Set<Integer> hash = new HashSet<Integer>();
        
        queue.offer(0);
        hash.add(0);
        
        while(!queue.isEmpty()){
            int node = queue.poll();
            
            for(Integer neighbor:graph.get(node)){
                if(hash.contains(neighbor)){
                    continue;
                }
                hash.add(neighbor);
                queue.offer(neighbor);
            }
        }
        
        return hash.size()==n;
     }
     
     private Map<Integer,Set<Integer>> initializeGraph(int n,int[][] edges){
         Map<Integer,Set<Integer>> graph = new HashMap<>();
         
         for(int i=0;i<n;++i){
             graph.put(i,new HashSet<Integer>());
         }
         
         for(int i=0;i<edges.length;++i){
             int u = edges[i][0];
             int v = edges[i][1];
             
             graph.get(u).add(v);
             graph.get(v).add(u);
         }
         
         return graph;
     }
}
```

