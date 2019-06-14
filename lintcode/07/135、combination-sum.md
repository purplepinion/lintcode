```java
/*
135. 数字组合
中文English
给定一个候选数字的集合 candidates 和一个目标值 target. 找到 candidates 中所有的和为 target 的组合.

在同一个组合中, candidates 中的某个数字不限次数地出现.

样例
样例 1:

输入: candidates = [2, 3, 6, 7], target = 7
输出: [[7], [2, 2, 3]]
样例 2:

输入: candidates = [1], target = 3
输出: [[1, 1, 1]]
注意事项
所有数值 (包括 target ) 都是正整数.
返回的每一个组合内的数字必须是非降序的.
返回的所有组合之间可以是任意顺序.
解集不能包含重复的组合.
*/
public class Solution {
    /**
     * @param candidates: A list of integers
     * @param target: An integer
     * @return: A list of lists of integers
     */
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        
        List<List<Integer>> results = new ArrayList<>();
        
        if(candidates==null||candidates.length==0){
            return results;
        }
        
        List<Integer> conbination = new ArrayList<Integer>();
        
        //sort
        Arrays.sort(candidates);
        conbinationHelper(results,conbination,candidates,0,target);
        
        return results;
    }
    //1.递归定义
    private void conbinationHelper(
        List<List<Integer>> results,
        List<Integer> conbination,
        int[] candidates,
        int startIndex,
        int leftTarget
        ){
        
        //3.递归出口
        if(leftTarget==0){
            results.add(new ArrayList<Integer>(conbination));
        }
    
        
        //2.递归分解
        for(int i=startIndex;i<candidates.length;++i){
            
            //停止深度搜索
            if(leftTarget<candidates[startIndex]){
                break;
            }
            
            //去重
            if(i!=0&&candidates[i]==candidates[i-1]){
                continue;
            }
            conbination.add(candidates[i]);
            conbinationHelper(results,conbination,candidates,i,leftTarget-candidates[i]);
            conbination.remove(conbination.size()-1);
        }
    }
    
    
}
```

