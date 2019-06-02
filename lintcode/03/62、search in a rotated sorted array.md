```java
/*
62. 搜索旋转排序数组
中文English
假设有一个排序的按未知的旋转轴旋转的数组(比如，0 1 2 4 5 6 7 可能成为4 5 6 7 0 1 2)。给定一个目标值进行搜索，如果在数组中找到目标值返回数组中的索引位置，否则返回-1。你可以假设数组中不存在重复的元素。

样例
例1:

输入: [4, 5, 1, 2, 3] and target=1, 
输出: 2.
例2:

输入: [4, 5, 1, 2, 3] and target=0, 
输出: -1.
挑战
O(logN) 时间限制 最好一次二分法
*/

/*思路1：先用一次二分找出[4, 5, 1, 2, 3]，1的index，
再在[4,5] [1,2,3] 中分别用二分。
*/
/*
思路2：[4, 5, 6,7,1, 2, 3]
6
分为4个区间，[start,mid][mid,end0][start0,mid][mid,end]
每次确定区间，缩小范围
*/
public class Solution {
    /**
     * @param A: an integer rotated sorted array
     * @param target: an integer to be searched
     * @return: an integer
     */
    public int search(int[] A, int target) {
        if(A==null||A.length==0) return -1;
        
        int start = 0;
        int end = A.length-1;
        
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            
            if(A[mid]==target) return mid;
            //[4,5,6,7,7,1,1,2,3]
            if(A[start]<A[mid]){//mid在[4,5,6,7,7]中
                if(A[start]<=target&&target<=A[mid]){//target在[start，mid]中end=mid
                    end = mid;
                }else{//target在[mid,end0]中start=mid
                    start = mid;
                }
            }else{//mid在[1,1,2,3]中
                if(A[mid]<=target&&target<=A[end]){//target在[mid，end]中start=mid
                    start = mid;
                }else{//target在[start0,mid]中end=mid
                    end = mid;
                }
            }
        }
        
        if(A[start]==target) return start;
        if(A[end]==target) return end;
        
        return -1;
    }
}
```

