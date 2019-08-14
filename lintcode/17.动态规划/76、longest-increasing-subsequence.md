```java
76. 最长上升子序列
中文English
给定一个整数序列，找到最长上升子序列（LIS），返回LIS的长度。

样例
样例 1:
	输入:  [5,4,1,2,3]
	输出:  3
	
	解释:
	LIS 是 [1,2,3]


样例 2:
	输入: [4,2,4,5,3,7]
	输出:  4
	
	解释: 
	LIS 是 [2,4,5,7]
挑战
要求时间复杂度为O(n^2) 或者 O(nlogn)

说明
最长上升子序列的定义：

最长上升子序列问题是在一个无序的给定序列中找到一个尽可能长的由低到高排列的子序列，这种子序列不一定是连续的或者唯一的。
https://en.wikipedia.org/wiki/Longest_increasing_subsequence
public class Solution {
    /**
     * @param nums: An integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        
        if(nums==null || nums.length==0){
            return 0;
        }
        
        int len = nums.length;
        int[] maxLength = new int[len];
        
        for (int i=0;i<len;i++ ){
            maxLength[i] = 1;
        } 
        
        for(int i=1;i<len;i++){
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j]){
                    maxLength[i] = Math.max(maxLength[i],maxLength[j]+1);
                }
            }
        }
        
        int maxLen = 0;
        for(int i=0;i<len;i++){
            if(maxLength[i]>maxLen){
                maxLen = maxLength[i];
            }
        }
        
        return maxLen;
    }
}
```

