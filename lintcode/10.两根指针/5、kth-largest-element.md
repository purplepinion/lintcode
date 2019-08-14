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
    
    /*
    运用二分的思想，不断缩小问题的规模，平均时间复杂度达到O(n)
    */
    public int kthLargestElement(int n, int[] nums) {
        if(nums==null||nums.length==0||n<1||n>nums.length){
            return -1;
        }
        return findKthNum(nums,0,nums.length-1,n);
    }
    
    private int findKthNum(int[] nums,int start,int end,int k){
        if(start==end){
            return nums[start];
        }
        
        int i = start;
        int j = end;
        int povit = nums[start+(end-start)/2];
        
        while(i<=j){
            while(i<=j&&nums[i]>povit){
                i++;
            }
            while(i<=j&&nums[j]<povit){
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
        
        //[start j][j+1][i end] 
        //在左边部分
        if(start+(k-1)<=j){
            return findKthNum(nums,start,j,k);
        }
        
        //在右边部分
        if(start+(k-1)>=i){
            return findKthNum(nums,i,end,k-(i-start));
        }
        
        //在中间
        return nums[j+1];
    }
}
```

