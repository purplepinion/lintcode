```java
/*
64. 合并排序数组
中文English
合并两个排序的整数数组A和B变成一个新的数组。

样例
样例 1:

输入：[1, 2, 3]  3  [4,5]  2
输出：[1,2,3,4,5]
解释:
经过合并新的数组为[1,2,3,4,5]
样例 2:

输入：[1,2,5] 3 [3,4] 2
输出：[1,2,3,4,5]
解释：
经过合并新的数组为[1,2,3,4,5]
注意事项
你可以假设A具有足够的空间（A数组的大小大于或等于m+n）去添加B中的元素
*/
public class Solution {
    /*
     * @param A: sorted integer array A which has m elements, but size of A is m+n
     * @param m: An integer
     * @param B: sorted integer array B which has n elements
     * @param n: An integer
     * @return: nothing
     */
    public void mergeSortedArray(int[] A, int m, int[] B, int n) {
        int leftIndex = m-1;
        int rightIndex = n-1;
        int index = m+n-1;
        
        while(leftIndex>=0&&rightIndex>=0){
            if(A[leftIndex]>B[rightIndex]){
                A[index--] = A[leftIndex--];
            }else{
                A[index--] = B[rightIndex--];
            }
        }
        
        while(leftIndex>=0){
            A[index--] = A[leftIndex--];
        }
        
        while(rightIndex>=0){
            A[index--] = B[rightIndex--];
        }
    }
    

}
```

