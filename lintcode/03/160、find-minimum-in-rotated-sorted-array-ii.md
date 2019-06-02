```java
/*

160. 寻找旋转排序数组中的最小值 II
中文English
假设一个旋转排序的数组其起始位置是未知的（比如0 1 2 4 5 6 7 可能变成是4 5 6 7 0 1 2）。

你需要找到其中最小的元素。

样例
样例 1:

输入 :[2,1]
输出 : 1.
样例 2:

输入 :[4,4,5,6,7,0,1,2]
输出: 0.
注意事项
The array may contain duplicates.
*/

public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        if(nums==null|nums.length==0) return -1;
        
        int start = 0;
        int end = nums.length - 1;
        //[4,5,6,7,1,1,2,3]
        while(start + 1 < end){
            int mid = start + (end -start)/2;
            //mid在[1,1,2,3]中end=mid
            if(nums[mid]<nums[end]){
                end = mid;
            }else if(nums[mid]>nums[end]){//mid在[4,5,6,7]中start=mid
                start = mid;
            }else{//mid在[1,1]中end--
                end--;
            }
        }
        
        return nums[start]<nums[end]?nums[start]:nums[end];
    }
}
```

