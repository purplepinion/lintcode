```java
602. 俄罗斯套娃信封
中文English
给一定数量的信封，带有整数对 (w, h) 分别代表信封宽度和高度。一个信封的宽高均大于另一个信封时可以放下另一个信封。
求最大的信封嵌套层数。

样例
样例 1:

输入：[[5,4],[6,4],[6,7],[2,3]]
输出：3
解释：
最大的信封嵌套层数是 3 ([2,3] => [5,4] => [6,7])。
样例 2:

输入：[[4,5],[4,6],[6,7],[2,3],[1,1]]
输出：4
解释：
最大的信封嵌套层数是 4 ([1,1] => [2,3] => [4,5] / [4,6] => [6,7])。
public class Solution {
    /*
     * @param envelopes: a number of envelopes with widths and heights
     * @return: the maximum number of envelopes
     */
    public int maxEnvelopes(int[][] envelopes) {
        
        if(envelopes==null || envelopes.length==0 || envelopes[0].length==0){
            return 0;
        }
        
        quickSort(envelopes,0,envelopes.length-1);
        
        int len = envelopes.length;
        int[] maxLayers = new int[len];
        
        for(int i=0;i<len;i++){
            maxLayers[i] = 1;
        }
        
        for(int i=1;i<len;i++){
            for(int j=0;j<i;j++){
                if(envelopes[i][1]>envelopes[j][1]&&envelopes[i][0]!=envelopes[j][0]){
                    maxLayers[i] = Math.max(maxLayers[i],maxLayers[j]+1);
                }
            }
        }
        
        int result = 0;
        for(int i=0;i<len;i++){
            if(maxLayers[i]>result){
                result = maxLayers[i];
            }
        }
        
        return result;
        
    }
    
    private void quickSort(int[][]envelopes,int start,int end){
        if(start >= end){
            return ;
        }
        
        int left = start;
        int right = end;
        int mid = left + (right - left)/2;
        int povit = envelopes[mid][0];
        
        while(left<=right){
            while(left<=end&&envelopes[left][0]<povit){
                left++;
            }
            while(left<=right&&envelopes[right][0]>povit){
                right--;
            }
            
            if(left<=right){
                swap(envelopes,left,right);
                left++;
                right--;
            }
        }
        
        quickSort(envelopes,start,right);
        quickSort(envelopes,left,end);
    }
    
    private void swap(int[][] envelopes,int i,int j){
        int temp0 = envelopes[j][0];
        int temp1 = envelopes[j][1];
        envelopes[j][0] = envelopes[i][0];
        envelopes[j][1] = envelopes[i][1];
        envelopes[i][0] = temp0;
        envelopes[i][1] = temp1;
    }
}
```

