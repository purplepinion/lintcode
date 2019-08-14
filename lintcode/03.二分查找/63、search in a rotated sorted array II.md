```java
/*63. 搜索旋转排序数组 II
中文English
跟进“搜索旋转排序数组”，假如有重复元素又将如何？

是否会影响运行时间复杂度？

如何影响？

为何会影响？

写出一个函数判断给定的目标值是否出现在数组中。

样例
例1:

输入:
[]
1
输出:
false
例2:

输入:
[3,4,4,5,7,0,1,2]
4
输出:
true*/
/*思路1：[4,4,5,5,6,6,-1,1,1,2,2,3,3,4,4]
-1
将输入数组变成[4,5,6,-1,1,2,3,4],时间复杂度O(n),再用二分法O(logN)
思路2：暴力求解，时间复杂度O(n)
*/

public class Solution {
    /**
     * @param A: an integer ratated sorted array and duplicates are allowed
     * @param target: An integer
     * @return: a boolean 
     */
    public boolean search(int[] A, int target) {
        
        if(A==null||A.length==0) return false;
        
        for(int i=0;i<A.length;++i){
            if(A[i]==target) return true;
        }
        
        return false;
    }
}
```

