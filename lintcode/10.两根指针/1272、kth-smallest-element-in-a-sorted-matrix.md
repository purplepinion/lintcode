```java
1272. 有序矩阵中的第K小元素
中文English
给定一个 n x n 矩阵，每一行和每一列都按照升序排序，找出矩阵中的第 k 小元素。

注意是需要找将所有元素有序排列的第 k 小元素，而不是第 k 个互不相同的元素。

样例
样例1

输入：
[[ 1,  5,  9],[10, 11, 13],[12, 13, 15]]
8
输出： 13
样例2

输入：
[[-5]]
1
输出： -5
挑战
如果 k << n^2，最好的算法是什么？
如果 k ~ n^2 呢？

注意事项
你可以认为 k 始终是合法的，也就是说，1 ≤ k ≤ n^2。
public class Solution {
    /**
     * @param matrix: List[List[int]]
     * @param k: a integer
     * @return: return a integer
     */
    public int kthSmallest(int[][] matrix, int k) {
        if(matrix==null||matrix.length==0||matrix[0]==null||matrix[0].length==0||k<1||k>matrix.length*matrix[0].length){
            return -1;
        }
        
        return kthSmallestHelper(matrix,0,matrix.length*matrix[0].length-1,k);
    }
    
    private int kthSmallestHelper(int[][] matrix,int start,int end,int k){
        
        //int rows = matrix.length;
        int cols = matrix[0].length;
        
        if(start==end) {
            return matrix[start/cols][start%cols];
        }
        
        int i = start;
        int j = end;
        int mid = start + (end - start)/2;
        int povit = matrix[mid/cols][mid%cols];
        
        while(i<=j){
            while(i<=j&&matrix[i/cols][i%cols]<povit){
                i++;
            }
            while(i<=j&&matrix[j/cols][j%cols]>povit){
                j--;
            }
            
            if(i<=j){
                int temp = matrix[i/cols][i%cols];
                matrix[i/cols][i%cols] = matrix[j/cols][j%cols];
                matrix[j/cols][j%cols] = temp;
                j--;
                i++;
            }
        }
        
        if(start + (k-1) <= j){
            return kthSmallestHelper(matrix,start,j,k);
        }
        
        if(start + (k-1) >= i){
            return kthSmallestHelper(matrix,i,end,k - (i - start));
        }
        
        return matrix[(j+1)/cols][(j+1)%cols];
    }
}
```

