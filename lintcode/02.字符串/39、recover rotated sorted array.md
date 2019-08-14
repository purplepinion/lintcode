```java
/*
给定一个旋转排序数组，在原地恢复其排序。

样例
Example1:
[4, 5, 1, 2, 3] -> [1, 2, 3, 4, 5]
Example2:
[6,8,9,1,2] -> [1,2,6,8,9]

挑战
使用O(1)的额外空间和O(n)时间复杂度

说明
什么是旋转数组？

比如，原始数组为[1,2,3,4], 则其旋转数组可以是[1,2,3,4], [2,3,4,1], [3,4,1,2], [4,1,2,3]
*/
public class Solution {
    /**
     * @param nums: An integer array
     * @return: nothing
     */
    public void recoverRotatedSortedArray(List<Integer> nums) {
        if(nums==null||nums.size()==0) return;
        int len = nums.size();
        
        int index = 0;
        for(index=0;index<len;++index){
            if(index+1<len&&nums.get(index)>nums.get(index+1)){
                rotateHelper(nums,0,index);
                rotateHelper(nums,index+1,len-1);
                rotateHelper(nums,0,len-1);
                return ;
            }
        }
        
    }
    
    private void rotateHelper(List<Integer> nums,int start,int end){
        while(start<end){
            Integer temp = nums.get(start);
            nums.set(start,nums.get(end));
            nums.set(end,temp);
            start++;
            end--;
        }
    }
}
```

