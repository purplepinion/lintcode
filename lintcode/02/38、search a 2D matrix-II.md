```java
/*
写出一个高效的算法来搜索m×n矩阵中的值，返回这个值出现的次数。

这个矩阵具有以下特性：

每行中的整数从左到右是排序的。
每一列的整数从上到下是排序的。
在每一行或每一列中没有重复的整数。
[[1, 3, 5, 7],[2, 4, 7, 8],[3, 5, 9, 10]]
3

要求O(m+n) 时间复杂度和O(1) 额外空间
*/
public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @param target: An integer you want to search in matrix
     * @return: An integer indicate the total occurrence of target in the given matrix
     */
    public int searchMatrix(int[][] matrix, int target) {
        if(matrix==null||matrix.length==0) return 0;
        int n = matrix.length;
        
        if(matrix[0]==null||matrix.length==0) return 0;
        int m = matrix[0].length;
        
        int row = 0;
        int col = m-1;
        int count = 0;
        
        while(row<n&&col>=0){
            if(matrix[row][col]>target){
                col--;
            }
            else if(matrix[row][col]<target){
                row++;
            }
            else{
                count++;
                row++;
                col--;
            }
        }
        
        return count;
    }
}
```

