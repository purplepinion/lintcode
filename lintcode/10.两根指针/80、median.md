```java
80. 中位数
中文English
给定一个未排序的整数数组，找到其中位数。

中位数是排序后数组的中间值，如果数组的个数是偶数个，则返回排序后数组的第N/2个数。

样例
样例 1:

输入：[4, 5, 1, 2, 3]
输出：3
解释：
经过排序，得到数组[1,2,3,4,5]，中间数字为3
样例 2:

输入：[7, 9, 4, 5]
输出：5
解释：
经过排序，得到数组[4,5,7,9]，第二个(4/2)数字为5
挑战
时间复杂度为O(n)

注意事项
数组大小不超过10000
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer denotes the middle number of the array
     */
     
    /*
    ·子序列S中有K个数，此时pivot位置即为第K大的数，返回
    ·子序列S中的数字个数小于K，假设个数为L，则需要子序列T中继续递归划分出来前(K-L)个数
    ·子序列S中的数字个数大于K，则需要子序列S中继续递归划分出来前K个数
    */
    public int median(int[] nums) {
        // write your code here
        return findKthHelper(nums,0,nums.length-1,(nums.length+1)/2);
    }
    
    private int findKthHelper(int[] nums,int start,int end,int pos){
        
        if(start==end){
            return nums[start];
        }
        
        int  i = start;
        int j = end;
        int povit = nums[start + (end - start) / 2];
        
        while(i<=j){
            while(i<=j&&nums[i]<povit){
                i++;
            }
            while(i<=j&&nums[j]>povit){
                j--;
            }
            
            if(i<=j){
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
                j--;
                i++;
            }
        }
        
        if(start + (pos - 1) <= j){
            return findKthHelper(nums,start,j,pos);
        }
        
        if(start + (pos -1) >= i){
            return findKthHelper(nums,i,end,pos - (i - start));
        }
        
        return nums[j+1];
    }
}
```

