```java
/*
15. 全排列
中文English
给定一个数字列表，返回其所有可能的排列。

样例
样例 1：

输入：[1]
输出：
[
  [1]
]
样例 2：

输入：[1,2,3]
输出：
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
挑战
使用递归和非递归分别解决。

注意事项
你可以假设没有重复数字。
*/
public class Solution {
    /*
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        
        if(nums==null) return results;
        
        //
        if(nums.length==0) {
            results.add(new ArrayList<Integer>());
            return results;
        }
        Arrays.sort(nums);
        
        List<Integer> subRes = new ArrayList<>();
        Set<Integer> hash = new HashSet<Integer>();
        
        Helper(results,subRes,nums,hash);
        
        return results;
    }
    
    private void Helper(
        List<List<Integer>> results,
        List<Integer> subRes,
        int[] nums,
        Set<Integer> hash
        ){
        
        if(subRes.size()==nums.length){
            results.add(new ArrayList<Integer>(subRes));
            return;
        }
        
        for(int i=0;i<nums.length;++i){
            if(hash.contains(nums[i])){
                continue;
            }
            subRes.add(nums[i]);
            hash.add(nums[i]);
            Helper(results,subRes,nums,hash);
            hash.remove(nums[i]);
            subRes.remove(subRes.size()-1);
        }
        
    }
}
```

