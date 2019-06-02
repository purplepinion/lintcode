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
        if(A==null||A.length==0) return ;
        
        quickSort(A,0,A.length-1);
    }
    
    private void quickSort(int[] A,int start,int end){
        if(start>=end){
            return ;
        }
        //[3,2,1,4,5]
        int left =start;
        int right = end;
        int mid = start + (end - start)/2;
        //1.选取中心点作为划分点
        int povit = A[mid];
        //2.用left<=right是为了划分的两个区间边界没有交叉，避免死循环
        while(left<=right){
            //3.用A[left]<povit是为了均分相等元素提高效率
            while(left<=right&&A[left]<povit) left++;
            while(left<=right&&A[right]>povit) right--;
            if(left<=right){
                int temp = A[left];
                A[left] = A[right];
                A[right] = temp;
                left++;
                right--;
            }
        }
        //4.注意分成区间边界
        quickSort(A,start,right);
        quickSort(A,left,end);
    }
    
    
}
```

