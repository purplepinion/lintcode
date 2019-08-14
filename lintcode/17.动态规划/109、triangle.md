```java
109. 数字三角形
中文English
给定一个数字三角形，找到从顶部到底部的最小路径和。每一步可以移动到下面一行的相邻数字上。

样例
样例 1

输入下列数字三角形：
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
输出： 11
解释： 从顶到底部的最小路径和为11 ( 2 + 3 + 5 + 1 = 11)。
样例 2

输入下列数字三角形：
[
     [2],
    [3,2],
   [6,5,7],
  [4,4,8,1]
]
输出： 12
解释： 从顶到底部的最小路径和为12 ( 2 + 2 + 7 + 1 = 12)。
注意事项
如果你只用额外空间复杂度O(n)的条件下完成可以获得加分，其中n是数字三角形的总行数。


//自顶向下
public class Solution {
    
    public int minimumTotal(int[][] triangle) {
        
        if(triangle==null||triangle.length==0||triangle[0]==null||triangle[0].length==0){
            return -1;
        }
        
        int[][] f = new int[triangle.length][triangle.length];
        
        //初始化
        f[0][0] = triangle[0][0];
        for(int i=1;i<triangle.length;i++){
            f[i][0] = f[i-1][0] + triangle[i][0];
            f[i][i] = f[i-1][i-1] + triangle[i][i];
        }
        
        for(int i=1;i<triangle.length;i++){
            for(int j=1;j<i;j++){
                f[i][j] = Math.min(f[i-1][j-1],f[i-1][j]) + triangle[i][j];
            }
        }
        
        int shortPath = f[triangle.length-1][0];
        
        for(int i=1;i<triangle.length;i++){
            if(f[triangle.length-1][i]<shortPath){
                shortPath = f[triangle.length-1][i];
            }
        }
      
      return shortPath;
    }
    
}
```

