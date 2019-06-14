```java
Given a undirected graph, a node and a target, return the nearest node to given node which value of it is target, return NULL if you can’t find.

There is a mapping store the nodes’ values in the given parameters.

Notice

It’s guaranteed there is only one available solution

Have you met this question in a real interview? Yes 
Example 
2——--3 5 
\    | | 
 \   | | 
  \  | | 
   \ | | 
    1 –4 
Give a node 1, target is 50

there a hash named values which is [3,4,10,50,50], represent: 
Value of node 1 is 3 
Value of node 2 is 4 
Value of node 3 is 10 
Value of node 4 is 50 
Value of node 5 is 50

Return node 4

这道题目基本上就是一个变形后的BFS，因此并不困难 

/**
 * Definition for graph node.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */


public class Solution {
    /*
     * @param graph: a list of Undirected graph node
     * @param values: a hash mapping, <UndirectedGraphNode, (int)value>
     * @param node: an Undirected graph node
     * @param target: An integer
     * @return: a node
     */
    public UndirectedGraphNode searchNode(ArrayList<UndirectedGraphNode> graph,
                                          Map<UndirectedGraphNode, Integer> values,
                                          UndirectedGraphNode node,
                                          int target) {
        // write your code here
        if (node == null) {
            return null;
        }
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        queue.offer(node);
        while (!queue.isEmpty()) {
            UndirectedGraphNode root = queue.poll();
            if (values.get(root) == target) {
                return root;
            }
            for (UndirectedGraphNode val : root.neighbors) {
                queue.offer(val);
            }
        }
        return null;
    }
}
https://www.lintcode.com/problem/number-of-islands/description
https://www.lintcode.com/problem/build-post-office-ii/description
https://www.cnblogs.com/aprilyang/p/6505037.html
https://www.cnblogs.com/aprilyang/p/6505178.html
```

