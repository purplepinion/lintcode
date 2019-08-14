```java

56. 两数之和
中文English
给一个整数数组，找到两个数使得他们的和等于一个给定的数 target。

你需要实现的函数twoSum需要返回这两个数的下标, 并且第一个下标小于第二个下标。注意这里下标的范围是 0 到 n-1。

样例
Example1:
给出 numbers = [2, 7, 11, 15], target = 9, 返回 [0, 1].
Example2:
给出 numbers = [15, 2, 7, 11], target = 9, 返回 [1, 2].
挑战
Either of the following solutions are acceptable:

O(n) Space, O(nlogn) Time
O(n) Space, O(n) Time
注意事项
你可以假设只有一组答案。
public class Solution {
    /**
     * @param numbers: An array of Integer
     * @param target: target = numbers[index1] + numbers[index2]
     * @return: [index1, index2] (index1 < index2)
     */
    public int[] twoSum(int[] numbers, int target) {
        Map<Integer,Integer> map = new HashMap<Integer,Integer>();
        
        for(int i=0;i<numbers.length;i++){
            if(map.get(numbers[i])!=null){
                int[] ans = {map.get(numbers[i]),i};
                return ans;
            }
            
            map.put(target-numbers[i],i);
        }
        
        int[] ans = {};
        return ans;
    }
    
}
```

