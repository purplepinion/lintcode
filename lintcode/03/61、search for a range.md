```java
/*
61. 搜索区间
中文English
给定一个包含 n 个整数的排序数组，找出给定目标值 target 的起始和结束位置。

如果目标值不在数组中，则返回[-1, -1]

样例
例1:

输入:
[]
9
输出:
[-1,-1]

例2:

输入:
[5, 7, 7, 8, 8, 10]
8
输出:
[3, 4]
挑战
时间复杂度 O(log n)


*/
public class Solution {
    /**
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: a list of length 2, [index1, index2]
     */
    public int[] searchRange(int[] A, int target) {
        int[] range = new int[]{-1,-1};
        
        if(A==null||A.length==0) return range;
        
        int start = 0;
        int end = A.length-1;
        
        range[0] = helper0(A,start,end,target);
        range[1] = helper1(A,start,end,target);
        
        return range;
    }
    
    private int helper0(int[] nums,int start,int end,int target){
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            
            if(nums[mid]==target){
                end = mid;
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
    
    private int helper1(int[] nums,int start,int end,int target){
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            
            if(nums[mid]==target){
                start = mid;
            }else if(nums[mid]>target){
                end = mid;
            }else if(nums[mid]<target){
                start = mid;
            }
        }
        
        if(nums[end]==target) return end;
        if(nums[start]==target) return start;
        
        return -1;
    }
    
}
```

​	