```java
/*
433. 岛屿的个数
中文English
给一个 01 矩阵，求不同的岛屿的个数。

0 代表海，1 代表岛，如果两个 1 相邻，那么这两个 1 属于同一个岛。我们只考虑上下左右为相邻。

样例
Example 1:

Input:
[
  [1,1,0,0,0],
  [0,1,0,0,1],
  [0,0,0,1,1],
  [0,0,0,0,0],
  [0,0,0,0,1]
]
Output:
3
Example 2:

Input:
[
  [1,1]
]
Output:
1
*/
public class Solution {
    /**
     * @param grid: a boolean 2D matrix
     * @return: an integer
     */
    public int numIslands(boolean[][] grid) {
        
        if(grid==null||grid.length==0||grid[0].length==0) return 0;
        
        int row = grid.length-1;
        int col = grid[0].length-1;
        int islands = 0;
        for(int i=0;i<=row;++i){
            for(int j=0;j<=col;++j){
                if(grid[i][j]){
                    bfs(grid,i,j);
                    islands++;
                }
            }
        }
        
        return islands;
    }
    
    private void bfs(boolean[][] grid,int x,int y){
        int[] directionX = {1,-1,0,0};
        int[] directionY = {0,0,1,-1};
        
        Queue<Point> queue = new LinkedList<Point>();
        Point startPoint = new Point(x,y);
        queue.offer(startPoint);
        
        while(!queue.isEmpty()){
            Point partIsLand = queue.poll();
            for(int i=0;i<4;i++){
                Point adj = new Point(
                    partIsLand.x + directionX[i],
                    partIsLand.y + directionY[i]);
                    
                if(outOfBound(grid,adj.x,adj.y)){
                    continue;
                }
                
                if(grid[adj.x][adj.y]){
                    grid[adj.x][adj.y]=false;
                    queue.offer(adj);
                }
            }
        }
        
    }
    
    private boolean outOfBound(boolean[][] grid,int x,int y){
        int row = grid.length-1;
        int col = grid[0].length-1;
        
        return !(x>=0&&x<=row&&y>=0&&y<=col);
    }
}

class Point{
    public int x;
    public int y;
    
    public Point(int x,int y){this.x=x;this.y=y;}
}
```

