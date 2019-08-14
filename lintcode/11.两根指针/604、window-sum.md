```java
604. 滑动窗口内数的和
中文English
给你一个大小为n的整型数组和一个大小为k的滑动窗口，将滑动窗口从头移到尾，输出从开始到结束每一个时刻滑动窗口内的数的和。

样例
样例 1

输入：array = [1,2,7,8,5], k = 3
输出：[10,17,20]
解析：
1 + 2 + 7 = 10
2 + 7 + 8 = 17
7 + 8 + 5 = 20
    
public class Solution {
    /**
     * @param nums: a list of integers.
     * @param k: length of window.
     * @return: the sum of the element inside the window at each moving.
     */
    public int[] winSum(int[] nums, int k) {
        
        if(nums==null||nums.length==0||k>nums.length||k<1){
            return new int[0];
        }
        
        int len = nums.length;
        int pointer1 = 0;
        int pointer2 = k-1;
        
        
        int[] ans = new int[len - (k - 1)];
        ans[0] = 0;
        for(int i=pointer1;i<=pointer2;i++){
            ans[pointer1] += nums[i];
        }
        
        while(pointer2<len-1){
            pointer1++;
            pointer2++;
            ans[pointer1] = ans[pointer1-1] - nums[pointer1-1] + nums[pointer2];
        }
        
        return ans;
    }
}
```

