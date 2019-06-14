```java
/*

16. 带重复元素的排列
中文English
给出一个具有重复数字的列表，找出列表所有不同的排列。

样例
样例 1：

输入：[1,1]
输出：
[
  [1,1]
]
样例 2：

输入：[1,2,2]
输出：
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
挑战
使用递归和非递归分别完成该题。

*/
public class Solution {
    /*
     * @param :  A list of integers
     * @return: A list of unique permutations
     */
    public List<List<Integer>> permuteUnique(int[] nums) {
       List<List<Integer>> results = new ArrayList<>();
        
        if(nums==null) return results;
        
        //
        if(nums.length==0) {
            results.add(new ArrayList<Integer>());
            return results;
        }
        Arrays.sort(nums);
        
        List<Integer> subRes = new ArrayList<>();
        //访问数组
        boolean[] visited = new boolean[nums.length];
        
        Helper(results,subRes,nums,visited);
        
        return results;
    }
    
    private void Helper(
        List<List<Integer>> results,
        List<Integer> subRes,
        int[] nums,
        boolean[] visited
        ){
        
        if(subRes.size()==nums.length){
            results.add(new ArrayList<Integer>(subRes));
            return;
        }
        
        for(int i=0;i<nums.length;++i){
            
            //每个数在一次排列中只能出现一次
            if(visited[i]==true){
                continue;
            }
            
            //数字相等只选取相等数字排列的一种情况
            if(i!=0&&nums[i]==nums[i-1]&&visited[i-1]==true){
                continue;
            }
            subRes.add(nums[i]);
            visited[i] = true;
            Helper(results,subRes,nums,visited);
            visited[i] = false;
            subRes.remove(subRes.size()-1);
        }
        
    }
};
```

