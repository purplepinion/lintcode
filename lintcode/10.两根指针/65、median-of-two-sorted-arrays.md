```java
65. 两个排序数组的中位数
中文English
两个排序的数组A和B分别含有m和n个数，找到两个排序数组的中位数，要求时间复杂度应为O(log (m+n))。

样例
样例1

输入:
A = [1,2,3,4,5,6]
B = [2,3,4,5]
输出: 3.5
样例2

输入:
A = [1,2,3]
B = [4,5]
输出: 3
挑战
时间复杂度为O(log n)

说明
中位数的定义：

这里的中位数等同于数学定义里的中位数。
中位数是排序后数组的中间值。
如果有数组中有n个数且n是奇数，则中位数为A[(n-1)/2]A[(n−1)/2]。
如果有数组中有n个数且n是偶数，则中位数为 (A[n / 2] + A[n / 2 + 1]) / 2(A[n/2]+A[n/2+1])/2.
比如：数组A=[1,2,3]的中位数是2，数组A=[1,19]的中位数是10。

public class Solution {
    /*
     * @param A: An integer array
     * @param B: An integer array
     * @return: a double whose format is *.5 or *.0
     
     二分思想解决，在两个排序数组的最小值和最大值之间找到满足小于这个值的数刚好为总数的一半
     时间复杂度O(log(range)  * O(log(m * n))
     */
    public double findMedianSortedArrays(int[] A, int[] B) {
        int len = A.length + B.length;
        
        if(len%2==0){
            return (findKth(A,B,len/2) + findKth(A,B,len/2 + 1)) / 2.0;
        }else{
            return (findKth(A,B,len/2 + 1));
        }
    }
    
    //找到第k位数
    private double findKth(int[] A,int[] B,int k){
        
        if(A==null||A.length==0){
            return B[k-1];
        }
        
        if(B==null||B.length==0){
            return A[k-1];
        }
        
        int start = Math.min(A[0],B[0]);
        int end = Math.max(A[A.length-1],B[B.length-1]);
        
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            
            if(countOfLE(A,mid) + countOfLE(B,mid) < k){
                start = mid;
            }else{
                end = mid;
            }
        }
        
        if(countOfLE(A,start) + countOfLE(B,start) >= k){
            return start;
        }else{
            return end;
        }
    }
    
    
    //求出arr中小于等于povit的数的个数
    private int countOfLE(int[] arr,int povit){
        
        int start = 0;
        int end = arr.length-1;
        
        while(start + 1 < end){
            int mid = start + (end - start) / 2;
            
            if(arr[mid]<=povit){
                start = mid;
            }else{
                end = mid;
            }
        }
        
        //[0 start-1] [start end] [end len-1]
        if(arr[start] > povit){
            return start;
        }
        
        if(arr[end] > povit){
            return end;
        }
        
        return arr.length;
    }
}
```

