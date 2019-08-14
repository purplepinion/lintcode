```java

143. 排颜色 II
中文English
给定一个有n个对象（包括k种不同的颜色，并按照1到k进行编号）的数组，将对象进行分类使相同颜色的对象相邻，并按照1,2，...k的顺序进行排序。

样例
样例1

输入: 
[3,2,2,1,4] 
4
输出: 
[1,2,2,3,4]
样例2

输入: 
[2,1,1,2,2] 
2
输出: 
[1,1,2,2,2]
挑战
一个相当直接的解决方案是使用计数排序扫描2遍的算法。这样你会花费O(k)的额外空间。你否能在不使用额外空间的情况下完成？

注意事项
不能使用代码库中的排序函数来解决这个问题
k <= n
public class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        if(colors==null || colors.length==0){
            return ;
        }
        
        rainbowSort(colors,0,colors.length-1,1,k);
    }
    
    private void rainbowSort(int[] colors,
                        int left,
                        int right,
                        int fromColor,
                        int toColor){
        if(fromColor==toColor){
            return ;
        }
        
        if(left>=right){
            return ;
        }
        
        int colorMid = fromColor + (toColor - fromColor)/2;
        int l = left;
        int r = right;
        
        while(l < r){
            /*注意小于等于*/
            while(l < r && colors[l] <= colorMid){
                l++;
            }
            
            while(l < r && colors[r] > colorMid){
                r--;
            }
            
            if(l<r){
                int temp = colors[l];
                colors[l] = colors[r];
                colors[r] = temp;
                l++;
                r--;
            }
        }
        
        rainbowSort(colors,left,r,fromColor,colorMid);
        rainbowSort(colors,l,right,colorMid+1,toColor);
        
    }
}
```

