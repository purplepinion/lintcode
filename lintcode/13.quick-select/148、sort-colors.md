```java
148. 颜色分类
中文English
给定一个包含红，白，蓝且长度为 n 的数组，将数组元素进行分类使相同颜色的元素相邻，并按照红、白、蓝的顺序进行排序。

我们可以使用整数 0，1 和 2 分别代表红，白，蓝。

样例
样例 1

输入 : [1, 0, 1, 2]
输出 : [0, 1, 1, 2]
解释 : 原地排序。
挑战
一个相当直接的解决方案是使用计数排序扫描2遍的算法。

首先，迭代数组计算 0,1,2 出现的次数，然后依次用 0,1,2 出现的次数去覆盖数组。

你否能想出一个仅使用常数级额外空间复杂度且只扫描遍历一遍数组的算法？

注意事项
不能使用代码库中的排序函数来解决这个问题。
排序需要在原数组中进行。
public class Solution {
    /**
     * @param nums: A list of integer which is 0, 1 or 2 
     * @return: nothing
     */
    public void sortColors(int[] nums) {
        if(nums==null || nums.length==0){
            return ;
        }
        
        
        int left = 0;
        int right = nums.length - 1;
        int i = 0;
        
        while(i<right){
            if(nums[i]==0){
                swap(nums,left,i);
                left++;
                i++;
            }else if(nums[i]==2){
                swap(nums,right,i);
                right--;
            }else{
                i++;
            }
        }
        
    }
    
    private void swap(int nums[],int i,int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

