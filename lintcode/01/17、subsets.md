```java
public class Solution {
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     * 给定一个含不同整数的集合，返回其所有的子集。
     * 子集中的元素排列必须是非降序的，解集必须不包含重复的子集。
     * 深度优先搜索
     */
    /* 
    输入：[1,2,3]
    输出：
    [
      [3],
      [1],
      [2],
      [1,2,3],
      [1,3],
      [2,3],
      [1,2],
      []
    ]
    */
    public List<List<Integer>> subsets(int[] nums) {
        //ArrayList保存最后结果
        List<List<Integer>> results = new ArrayList<>();
        if(nums==null) return results;
        //先对数组排序
        Arrays.sort(nums);
        //中间变量记录每个排列
        ArrayList<Integer> subset = new ArrayList<>();
        subsetsHelper(nums,0,subset,results);
        return results;
    }
    
    private void subsetsHelper(int[] nums,
                            int startIndex,
                            ArrayList<Integer> subset,
                            List<List<Integer>> results)
    {
        //添加排列到results（深拷贝）
        results.add(new ArrayList<Integer>(subset));
        //深度优先搜索
        for(int i=startIndex;i<nums.length;++i){
            //添加一个元素到subset
            subset.add(nums[i]);
            //添加后一个元素
            subsetsHelper(nums,i+1,subset,results);
            //移除这个元素
            subset.remove(subset.size()-1);
        }
    }
}
```