```java
/*给出一个目标数字和一个升序整数数组，返回目标数字在数组中出现的次数。

给出 [1, 3, 3, 4, 5] 并且 target = 3, 返回 2.
给出 [2, 2, 3, 4, 6] 并且 target = 4, 返回 1
给出 [1, 2, 3, 4, 5] 并且 target = 6, 返回 0*/

public class Solution {
    /**
     * @param A: an integer sorted array
     * @param target: an integer to be inserted
     * @return: a list of length 2, [index1, index2]
     */
    public int[] searchTimesForTarget(int[] A, int target) {
        int times = 0;
        
        if(A==null||A.length==0) return times;
        
        int start = 0;
        int end = A.length-1;
        
        int first = helper0(A,start,end,target);
        int last = helper1(A,start,end,target);
        
        return last - first + 1;
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

