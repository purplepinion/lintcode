```java
144. 交错正负数
中文English
给出一个含有正整数和负整数的数组，重新排列成一个正负数交错的数组。

样例
样例 1

输入 : [-1, -2, -3, 4, 5, 6]
输出 : [-1, 5, -2, 4, -3, 6]
解释 : 或者仍和满足条件的答案 
挑战
完成题目，且不消耗额外的空间。

注意事项
不需要保持正整数或者负整数原来的顺序。
public class Solution {
    /*
     * @param A: An integer array.
     * @return: nothing
     */
    public void rerange(int[] A) {
        
        if(A==null || A.length<3){
            return ;
        }
        
        //默认正数不多于负数
        int pos = 1;
        int neg = 0;
        
        //正数放前面
        int countPos = 0;
        int posIndex = 0;
        for(int i=0;i<A.length;i++){
            if(A[i]>0){
                swap(A,posIndex,i);
                posIndex++;
                countPos++;
            }
        }
        //判断正数还是负数多,多的放在数组后面
        if(countPos>A.length/2){
            //正数多于负数
            pos = 0;
            neg = 1;
            for(int i=0,j=A.length-1;i<j;i++,j--){
                swap(A,i,j);
            }
        }
        
        //正负数交错
        while(pos<A.length&&neg<A.length){
            while(pos<A.length&&A[pos]>0){
                pos+=2;
            }
            while(neg<A.length&&A[neg]<0){
                neg+=2;
            }
            
            if(pos<A.length&&neg<A.length){
                swap(A,pos,neg);
            }
        }
        
    }
    
    private void swap(int[] A,int i,int j){
        int temp = A[i];
        A[i] = A[j];
        A[j] = temp;
    }
}
```

