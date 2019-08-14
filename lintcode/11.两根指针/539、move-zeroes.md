```java
539. 移动零
中文English
给一个数组 nums 写一个函数将 0 移动到数组的最后面，非零元素保持原数组的顺序

样例
例1:

输入: nums = [0, 1, 0, 3, 12],
输出: [1, 3, 12, 0, 0].
例2:

输入: nums = [0, 0, 0, 3, 1],
输出: [3, 1, 0, 0, 0].
注意事项
1.必须在原数组上操作
2.最小化操作数
public class Solution {
    /**
     * @param nums: an integer array
     * @return: nothing
     */
    public void moveZeroes(int[] nums) {
        if(nums==null||nums.length==0){
            return ;
        }
        
        int i=0,j=0;
        while(j<nums.length){
            if(nums[j]!=0){
                int temp = nums[j];
                nums[j] = nums[i];
                nums[i] = temp;
                i++;
            }
            j++;
        }
    }
}
```

