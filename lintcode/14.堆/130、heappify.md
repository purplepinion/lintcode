```java
130. 堆化
中文English
给出一个整数数组，堆化操作就是把它变成一个最小堆数组。

对于堆数组A，A[0]是堆的根，并对于每个A[i]，A [i * 2 + 1]是A[i]的左儿子并且A[i * 2 + 2]是A[i]的右儿子。

样例
样例 1

输入 : [3,2,1,4,5]
输出 : [1,2,3,4,5]
解释 : 返回任何一个合法的堆数组
挑战
O(n)的时间复杂度完成堆化

说明
什么是堆？ 什么是堆化？ 如果有很多种堆化的结果？

堆是一种数据结构，它通常有三种方法：push， pop 和 top。其中，“push”添加新的元素进入堆，“pop”删除堆中最小/最大元素，“top”返回堆中最小/最大元素。
把一个无序整数数组变成一个堆数组。如果是最小堆，每个元素A[i]，我们将得到A[i * 2 + 1] >= A[i]和A[i * 2 + 2] >= A[i]
返回其中任何一个。

public class Solution {
    /*
     * @param A: Given an integer array
     * @return: nothing
     */
    public void heapify(int[] A) {
        for(int i=0;i<A.length;i++){
            shiftUp(A,i);
        }
    }
    //左二字 2*i+1， 右儿子 2*i+2  父亲(i-1)/2  
    private void shiftUp(int[] A,int index){
        while(index!=0){
            int father = (index-1)/2;
            if(A[father]<=A[index]){
                break;
            }
            swap(A,father,index);
            index = father;
        }
    }
    
    private void swap(int[] A,int i,int j){
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
}
```

