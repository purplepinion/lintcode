```java
/*
463. 整数排序
中文English
给一组整数，按照升序排序，使用选择排序，冒泡排序，插入排序或者任何 O(n2) 的排序算法。

样例
样例  1:
	输入:  [3, 2, 1, 4, 5]
	输出:  [1, 2, 3, 4, 5]
	
	样例解释: 
	返回排序后的数组。

样例 2:
	输入:  [1, 1, 2, 1, 1]
	输出:  [1, 1, 1, 1, 2]
	
	样例解释: 
	返回排好序的数组。
*/
public class Solution {
    /**
     * @param A: an integer array
     * @return: nothing
     */
    public void sortIntegers(int[] A) {
        if(A==null||A.length==0){
            return ;
        }
        
        int[] temp = new int[A.length];
        mergeSort(A,0,A.length-1,temp);
    }
    
    private void mergeSort(int[] A,int start,int end,int[] temp){
        if(start>=end) return;
        
        mergeSort(A,start,start+(end-start)/2,temp);
        mergeSort(A,start + (end-start)/2+1,end,temp);
        
        merge(A,start,end,temp);
    }
    
    private void merge(int[] A,int start,int end,int[] temp){
        int mid = start + (end - start)/2;
        int leftIndex = start;
        int rightIndex = mid + 1;
        int index = start;
        
        while(leftIndex<=mid&&rightIndex<=end){
            if(A[leftIndex]<A[rightIndex]){
                temp[index++] = A[leftIndex++];
            }else{
                temp[index++] = A[rightIndex++];
            }
        }
        
        while(leftIndex<=mid){
            temp[index++] = A[leftIndex++];
        }
        
        while(rightIndex<=end){
            temp[index++] = A[rightIndex++];
        }
        
        for(int i=start;i<=end;++i){
            A[i] = temp[i];
        }
    }
}
```

