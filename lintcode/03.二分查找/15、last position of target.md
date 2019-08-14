```java
/*
14. 二分查找
中文English
给定一个排序的整数数组（升序）和一个要查找的整数target，用O(logn)的时间查找到target最后一次出现的下标（从0开始），如果target不存在于数组中，返回-1。

样例
样例  1:
	输入:[1,4,4,5,7,7,8,9,9,10]，1
	输出: 0
	
	样例解释: 
	第一次出现在第0个位置。

样例 2:
	输入: [1, 2, 3, 3, 4, 5, 10]，3
	输出: 3
	
	样例解释: 
	第一次出现在第3个位置
	
样例 3:
	输入: [1, 2, 3, 3, 4, 5, 10]，6
	输出: -1
	
	样例解释: 
	没有出现过6， 返回-1

挑战
如果数组中的整数个数超过了2^32，你的算法是否会出错？
*/
public class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The last position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        if(nums==null|nums.length==0) return -1;
        
        int start = 0;
        int end = nums.length-1;
        
        while(start+1 < end){
            int mid = start + (end - start)/2;
            if(nums[mid]==target){
                start = mid;
            }else if(nums[mid]>target){
                end = mid;
            }else if(nums[mid]<target){
                start = mid;   
            }
        }
        
        if(nums[start]==target) return start;
        
        if(nums[end]==target) return end;
        
        return -1;
    }
}
```

