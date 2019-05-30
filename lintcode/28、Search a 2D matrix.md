

```java
/*
写出一个高效的算法来搜索 m × n矩阵中的值。

这个矩阵具有以下特性：

每行中的整数从左到右是排序的。
每行的第一个数大于上一行的最后一个整数。
样例
样例  1:
	输入: [[5]],2
	输出: false
	
	样例解释: 
  没有包含，返回false。

样例 2:
	输入:  
[
  [1, 3, 5, 7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
],3
	输出: true
	
	样例解释: 
	包含则返回true。*/
public class Solution {
    /**
     * @param matrix: matrix, a list of lists of integers
     * @param target: An integer
     * @return: a boolean, indicate whether matrix contains target
     * O(log(n) + log(m)) 时间复杂度
     */
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix==null||matrix.length==0) return false;
        int n = matrix.length;
        
        if(matrix[0]==null||matrix[0].length==0) return false;
        int m = matrix[0].length;
        
        int start = 0;
        int end = n * m - 1;
        
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            int row = mid/m;
            int col = mid%m;
            
            if(matrix[row][col]<target){
                start = mid;
            }else{
                end = mid;
            }
        }
        
        if(matrix[start/m][start%m]==target) return true;
        if(matrix[end/m][end%m]==target) return true;
        
        return false;
    }
}
```