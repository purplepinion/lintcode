```java
114. 不同的路径
中文English
有一个机器人的位于一个 m × n 个网格左上角。

机器人每一时刻只能向下或者向右移动一步。机器人试图达到网格的右下角。

问有多少条不同的路径？

样例
Example 1:

Input: n = 1, m = 3
Output: 1	
Explanation: Only one path to target position.
Example 2:

Input:  n = 3, m = 3
Output: 6	
Explanation:
	D : Down
	R : Right
	1) DDRR
	2) DRDR
	3) DRRD
	4) RRDD
	5) RDRD
	6) RDDR
注意事项
n和m均不超过100


public class Solution {
    /**
     * @param m: positive integer (1 <= m <= 100)
     * @param n: positive integer (1 <= n <= 100)
     * @return: An integer
     */
     
    //(m+n)!/(m!+n!)
    public int uniquePaths(int m, int n) {
        
        int[][] pathKinds = new int[m][n];
        
        
        //初始化
        pathKinds[0][0] = 1;
        
        for(int i=1;i<m;i++){
            pathKinds[i][0] = 1;
        }
        
        for(int i=1;i<n;i++){
            pathKinds[0][i] = 1;
        }
        
        //状态求解
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                pathKinds[i][j] = pathKinds[i-1][j] + pathKinds[i][j-1];
            }
        }
        
        return pathKinds[m-1][n-1];
    }
}
```

