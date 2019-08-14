```java
Given a knight in a chessboard (a binary matrix with 0 as empty and 1 as barrier) with a source position, find the shortest path to a destinationposition, return the length of the route. 
Return -1 if knight can not reached.

 Notice
source and destination must be empty.
Knight can not enter the barrier.

 
Clarification
If the knight is at (x, y), he can get to the following positions in one step:

(x + 1, y + 2)
(x + 1, y - 2)
(x - 1, y + 2)
(x - 1, y - 2)
(x + 2, y + 1)
(x + 2, y - 1)
(x - 2, y + 1)
(x - 2, y - 1)
Example
[[0,0,0],
 [0,0,0],
 [0,0,0]]
source = [2, 0] destination = [2, 2] return 2

[[0,1,0],
 [0,0,0],
 [0,0,0]]
source = [2, 0] destination = [2, 2] return 6

[[0,1,0],
 [0,0,1],
 [0,0,0]]
source = [2, 0] destination = [2, 2] return -1
In this question, we can use bfs to find the shortest path. Each layer is a step. So for each layer, we should iterate every node in this layer and put their neighbors in the queue. We should use size to decide which layer it is instead of a new queue. Because a new queue will occupy to much memory. 
Besides, when the node is visited, we don't need a hashmap to record. Also because the memory issue.
 
复制代码
/**
 * Definition for a point.
 * public class Point {
 *     publoc int x, y;
 *     public Point() { x = 0; y = 0; }
 *     public Point(int a, int b) { x = a; y = b; }
 * }
 */
public class Solution {
    /**
     * @param grid a chessboard included 0 (false) and 1 (true)
     * @param source, destination a point
     * @return the shortest path 
     */
    public int shortestPath(boolean[][] grid, Point source, Point destination) {
    	if(grid==null||grid.legnth==0||grid[0].length==0) retuen -1;
    	
    	int[] dx = {1,1,-1,-1,2,2,-2,-2};
    	int[] dy = {2,-2,2,-2,1,-1,1,-1};
    	
    	Queue<Point> queue = new LinkedList<Point>();
    	queue.offer(source);
    	
    	int steps = 0;
        while(!queue.isEmpty()){
        	Point curPos = queue.poll();
            if(curPos.x == destination.x&&curPos.y == destination.y){
            	return steps;
            }
            for(int i=0;i<8;++i){
            	Point newPos = new Point(
            		curPos.x + dx[i],
            		curPos.y + dy[i]
            		);
            	
                if(!outOfBound(grid,newPos)&&!grid[newPos.x][newPos.y]){
                	queue.offer(newPos);
                	grid[newPos.x][newPos.y]=true;
                }
                
            }
            steps++;
        }
        
        return -1;	
  	}
  	
    private boolean outOfBound(boolean[][] grid,Point point){
    	int row = grid.length-1;
    	int col = grid[0].length-1;
    	
    	return !(point.x>=0&&point.y>=0&&point.x<=row&&point.y<=col);
    }
}
```

