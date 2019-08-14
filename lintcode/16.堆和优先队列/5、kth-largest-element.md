```java
5. 第k大元素
中文English
在数组中找到第 k 大的元素。

样例
样例 1：

输入：
n = 1, nums = [1,3,4,2]
输出：
4
样例 2：

输入：
n = 3, nums = [9,3,2,4,8]
输出：
4
挑战
要求时间复杂度为O(n)，空间复杂度为O(1)。

注意事项
你可以交换数组中的元素的位置
public class Solution {
    /**
     * quick select 解决
     */
    public int kthLargestElement(int n, int[] nums) {
        if(nums==null || nums.length==0 || n<1 || nums.length<n){
            return -1;
        }
        
        int left = 0;
        int right = nums.length-1;
        
        while(left<=right){
            int index = left - 1;
            //nums[left]到nums[index] > nums[right]
            for(int i=left;i<right;i++){
                if(nums[i]>nums[right]){
                    swap(nums,i,++index);
                }
            }
            swap(nums,right,++index);
            
            if(index == n-1){
                return nums[index];
            }else if(index < n-1){
                left = index + 1;
            }else{
                right = index - 1;
            }
        }
        
        return -1;
    }
    
    private void swap(int[] nums,int i,int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

