```java
608. 两数和 II-输入已排序的数组
中文English
给定一个已经 按升序排列 的数组，找到两个数使他们加起来的和等于特定数。
函数应该返回这两个数的下标，index1必须小于index2。注意返回的值不是 0-based。

样例
例1:

输入: nums = [2, 7, 11, 15], target = 9 
输出: [1, 2]
例2:

输入: nums = [2,3], target = 5
输出: [1, 2]
注意事项
你可以假设每个输入刚好只有一个答案
public class Solution {
    /**
     * @param nums: an array of Integer
     * @param target: target = nums[index1] + nums[index2]
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum(int[] nums, int target) {
        int[] ans = new int[2];
        
        if(nums==null||nums.length<2){
            return ans;
        }
        Arrays.sort(nums);
        int left = 0;
        int right = nums.length - 1;
        
        while(left < right){
            if(nums[left] + nums[right] == target){
                ans[0] = left + 1;
                ans[1] = right + 1;
                return ans;
            }
            
            if(nums[left] + nums[right] < target){
                left++;
            }else{
                right--;
            }
        }
        
        return ans;
    }
}


```

