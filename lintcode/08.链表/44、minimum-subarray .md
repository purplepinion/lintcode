```java
/*
44. 最小子数组
中文English
给定一个整数数组，找到一个具有最小和的连续子数组。返回其最小和。

样例
样例 1

输入：[1, -1, -2, 1]
输出：-3
样例 2

输入：[1, -1, -2, 1, -4]
输出：-6
注意事项
子数组最少包含一个数字
*/
public class Solution {
    /*
     * @param nums: a list of integers
     * @return: A integer indicate the sum of minimum subarray
     */
    public int minSubArray(List<Integer> nums) {
        if(nums==null||nums.size()==0) return 0;
        
        int min = Integer.MAX_VALUE;
        int max = 0;
        int curSum = 0;
        //当前min为之前min和cum-max中小的
        for(int i=0;i<nums.size();++i){
            curSum += nums.get(i);
            
            min = Math.min(min,curSum-max);
            max = Math.max(max,curSum);
        }
        
        return min;
    }
}
```

