```java
110. 最小路径和
中文English
给定一个只含非负整数的m*n网格，找到一条从左上角到右下角的可以使数字和最小的路径。



样例
样例 1:
	输入:  [[1,3,1],[1,5,1],[4,2,1]]
	输出: 7
	
	样例解释：
	路线为： 1 -> 3 -> 1 -> 1 -> 1。


样例 2:
	输入:  [[1,3,2]]
	输出:  6
	
	解释:  
	路线是： 1 -> 3 -> 2

注意事项
你在同一时间只能向下或者向右移动一步
public class Solution {
    
    public int minPathSum(int[][] grid) {
        if(grid==null || grid.length==0 || grid[0].length==0){
            return 0;
        }
        
        int rows = grid.length;
        int cols = grid[0].length;
        int[][] pathSum = new int[rows][cols];
        
        //初始化
        pathSum[0][0] = grid[0][0];
        
        for(int i=1;i<rows;i++){
            pathSum[i][0] = pathSum[i-1][0] + grid[i][0];
        }
        
        for(int i=1;i<cols;i++){
            pathSum[0][i] = pathSum[0][i-1] + grid[0][i];
        }
        
        //状态方程求解
        for(int i=1;i<rows;i++){
            for(int j=1;j<cols;j++){
                pathSum[i][j] = Math.min(pathSum[i-1][j],pathSum[i][j-1]) + grid[i][j];
            }
        }
        
        //结果
        return pathSum[rows-1][cols-1];
    }
}
```

