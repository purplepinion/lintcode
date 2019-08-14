```java
117. 跳跃游戏 II
中文English
给出一个非负整数数组，你最初定位在数组的第一个位置。

数组中的每个元素代表你在那个位置可以跳跃的最大长度。　　　

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

样例
样例 1

输入 : [2,3,1,1,4]
输出 : 2
解释 : 到达最后位置的最小跳跃次数是2(从下标0到1跳跃1个距离长度，然后跳跃3个距离长度到最后wei'z)
public class Solution {
    /**
     * @param A: A list of integers
     * @return: An integer
     */
    public int jump(int[] A) {
        if(A==null || A.length==0){
            return -1;
        }
        
        int len = A.length;

        
        boolean[] canReach = new boolean[len];
        int[] reachSteps = new int[len];
        
        for(int i=0;i<len;i++){
            reachSteps[i] = Integer.MAX_VALUE;
        }
        
        reachSteps[0] = 0;
        canReach[0] = true;
        
        
        for(int j=1;j<len && j<=A[0];j++){
            canReach[j] = true;
            reachSteps[j] = 1;
        }
        
        
        for(int i=1;i<len;i++){
            if(canReach[i]){
                for(int j=i+1;j<len && j<=i+A[i];j++){
                    canReach[j] = true;
                    reachSteps[j] = Math.min(reachSteps[i]+1,reachSteps[j]);
                }
            }
        }
        
        return reachSteps[len-1];
    }
}
```

