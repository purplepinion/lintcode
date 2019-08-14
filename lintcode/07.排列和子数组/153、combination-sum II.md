```java
/*

153. 数字组合 II
中文English
给定一个数组 num 和一个整数 target. 找到 num 中所有的数字之和为 target 的组合.

样例
样例 1:

输入: num = [7,1,2,5,1,6,10], target = 8
输出: [[1,1,6],[1,2,5],[1,7],[2,6]]
样例 2:

输入: num = [1,1,1], target = 2
输出: [[1,1]]
解释: 解集不能包含重复的组合
注意事项
在同一个组合中, num 中的每一个数字仅能被使用一次.
所有数值 (包括 target ) 都是正整数.
返回的每一个组合内的数字必须是非降序的.
返回的所有组合之间可以是任意顺序.
解集不能包含重复的组合.
*/
public class Solution {
    /**
     * @param num: Given the candidate numbers
     * @param target: Given the target number
     * @return: All the combinations that sum to target
     */
    public List<List<Integer>> combinationSum2(int[] num, int target) {
        
        List<List<Integer>> results = new ArrayList<>();
        
        if(num==null||num.length==0){
            return results;
        }
        
        
        List<Integer> combination = new ArrayList<>();
        //sort
        Arrays.sort(num);
        combinationHelper(results,combination,0,target,num);
        
        return results;
    }
    
    private void combinationHelper(
        List<List<Integer>> results,
        List<Integer> combination,
        int startIndex,
        int leftTarget,
        int[] num
        ){
            
        if(leftTarget==0){
            results.add(new ArrayList<Integer>(combination));
            return;
        }
        
        for(int i=startIndex;i<num.length;++i){
            if(leftTarget<num[i]){
                break;
            }
            //tips
            if(i!=0&&num[i]==num[i-1]&&i>startIndex){
                continue;
            }
            combination.add(num[i]);
            combinationHelper(results,combination,i+1,leftTarget-num[i],num);
            combination.remove(combination.size()-1);
        }
        
    }
}
```

