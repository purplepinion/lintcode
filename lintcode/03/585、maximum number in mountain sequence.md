```java
/*

585. 山脉序列中的最大值
中文English
给 n 个整数的山脉数组，即先增后减的序列，找到山顶（最大值）

样例
例1:

输入: nums = [1, 2, 4, 8, 6, 3] 
输出: 8
例2:

输入: nums = [10, 9, 8, 7], 
输出: 10
*/
public class Solution {
    /**
     * @param nums: a mountain sequence which increase firstly and then decrease
     * @return: then mountain top
     */
    public int mountainSequence(int[] nums) {
        if(nums==null||nums.length==0) return -1;
        
        int start = 0;
        int end = nums.length - 1;
        //长度为2不进循环
        while(start + 1 < end){
            int mid = start + (end - start)/2;
             //当nums为[0,1]时，mid=0，mid-1=-1，为什么没有数组越界异常
            if(nums[mid]>nums[mid-1]){
                start = mid;
            }else if(nums[mid]>nums[mid+1]){
                end = mid;
            }
        }
        
        return nums[start]>nums[end]?nums[start]:nums[end];
    }
}
```

