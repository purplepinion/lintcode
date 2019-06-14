```java
/*
138. 子数组之和
中文English
给定一个整数数组，找到和为零的子数组。你的代码应该返回满足要求的子数组的起始位置和结束位置

样例
样例 1:

输入: [-3, 1, 2, -3, 4]
输出: [0,2] 或 [1,3]	
样例解释： 返回任意一段和为0的区间即可。
样例 2:

输入: [-3, 1, -4, 2, -3, 4]
输出: [1,5]
注意事项
至少有一个子数组的和为 0
*/
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number and the index of the last number
     */
    public List<Integer> subarraySum(int[] nums) {
        //记录所有index位置的前面数之和sum，将sum，index-1存在hash中
        //若当前sum和之前某个index的sum相等，则index，curIndex则为所求区间
        
        int len = nums.length;
        
        ArrayList<Integer> ans = new ArrayList<>();
        Map<Integer,Integer> hash = new HashMap<Integer,Integer>();
        
        //初始sum=0，index=0
        hash.put(0,-1);
        
        int sum = 0;
        for(int i=0;i<len;++i){
            sum += nums[i];
            
            //containsKey()
            if(hash.containsKey(sum)){
                ans.add(hash.get(sum)+1);
                ans.add(i);
                return ans;
            }
            
            hash.put(sum,i);
        }
        
        return ans;
    }
}
```

