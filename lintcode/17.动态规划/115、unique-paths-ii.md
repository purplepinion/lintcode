```java
115. 不同的路径 II
中文English
"不同的路径" 的跟进问题：

现在考虑网格中有障碍物，那样将会有多少条不同的路径？

网格中的障碍和空位置分别用 1 和 0 来表示。

样例
Example 1:
	Input: [[0]]
	Output: 1


Example 2:
	Input:  [[0,0,0],[0,1,0],[0,0,0]]
	Output: 2
	
	Explanation:
	Only 2 different path.
	

注意事项
m 和 n 均不超过100
public class Solution {
    /**
     * @param obstacleGrid: A list of lists of integers
     * @return: An integer
     */
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if(obstacleGrid==null || obstacleGrid.length==0 || obstacleGrid[0].length==0){
            return 0;
        }
        
        int rows = obstacleGrid.length;
        int cols = obstacleGrid[0].length;
        
        int[][] pathKinds = new int[rows][cols];
        //初始化
        if(obstacleGrid[0][0]!=1){
            pathKinds[0][0] = 1;
        }else{
            pathKinds[0][0] = 0;
        }
        
        for(int i=1;i<rows;i++){
            if(obstacleGrid[i][0]!=1){
                pathKinds[i][0] = pathKinds[i-1][0];
            }else{
               pathKinds[i][0] = 0; 
            }
        }
        
        for(int i=1;i<cols;i++){
            if(obstacleGrid[0][i]!=1){
                pathKinds[0][i] = pathKinds[0][i-1];
            }else{
               pathKinds[0][i] = 0; 
            }
        }
        
        //状态求解
        for(int i=1;i<rows;i++){
            for(int j=1;j<cols;j++){
                if((obstacleGrid[i-1][j]==1 && obstacleGrid[i][j-1]==1) || obstacleGrid[i][j]==1){
                    pathKinds[i][j] = 0;
                }else if(obstacleGrid[i-1][j]==1){
                    pathKinds[i][j] = 0 + pathKinds[i][j-1];
                }else if(obstacleGrid[i][j-1]==1){
                    pathKinds[i][j] = pathKinds[i-1][j] + 0;
                }else{
                    pathKinds[i][j] = pathKinds[i-1][j] + pathKinds[i][j-1];
                }
                
            }
        }
        
        return pathKinds[rows-1][cols-1];
    }
}
```

