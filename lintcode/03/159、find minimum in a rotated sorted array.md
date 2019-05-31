```java
/*

159. 寻找旋转排序数组中的最小值
中文English
假设一个排好序的数组在其某一未知点发生了旋转（比如0 1 2 4 5 6 7 可能变成4 5 6 7 0 1 2）。你需要找到其中最小的元素。

样例
Example 1:

输入：[4, 5, 6, 7, 0, 1, 2]
输出：0
解释：
数组中的最小值为0
Example 2:

输入：[2,1]
输出：1
解释：
数组中的最小值为1
注意事项
你可以假设数组中不存在重复元素。
*/
public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        if(nums==null||nums.length==0) return -1;
        
        int start = 0;
        int end = nums.length-1;
        int target = nums[end];
        while(start+1<end){
            int mid = start + (end - start)/2;
            if(nums[mid]<=target){
                end = mid;
            }else if(nums[mid]>target){
                start = mid;
            }
        }
        
        if(nums[start]<=target) return nums[start];
        if(nums[end]<=target) return nums[end];
        
        return -1;
    }
}
```

