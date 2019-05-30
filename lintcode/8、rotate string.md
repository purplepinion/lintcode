```java
/*
给定一个字符串（以字符数组的形式给出）和一个偏移量，根据偏移量原地旋转字符串(从左向右旋转)

样例
样例 1:

输入:  str="abcdefg", offset = 3
输出:  str = "efgabcd"	
样例解释:  注意是原地旋转，即str旋转后为"efgabcd"
样例 2:

输入: str="abcdefg", offset = 0
输出: str = "abcdefg"	
样例解释: 注意是原地旋转，即str旋转后为"abcdefg"
样例 3:

输入: str="abcdefg", offset = 1
输出: str = "gabcdef"	
样例解释: 注意是原地旋转，即str旋转后为"gabcdef"
样例 4:

输入: str="abcdefg", offset =2
输出: str = "fgabcde"	
样例解释: 注意是原地旋转，即str旋转后为"fgabcde"
样例 5:

输入: str="abcdefg", offset = 10
输出: str = "efgabcd"	
样例解释: 注意是原地旋转，即str旋转后为"efgabcd"
挑战
在数组上原地旋转，使用O(1)的额外空间

注意事项
offset >= 0
str的长度 >= 0
*/
public class Solution {
    /**
     * @param str: An array of char
     * @param offset: An integer
     * @return: nothing
     */
    public void rotateString(char[] str, int offset) {
        if(str==null||str.length==0) return;
        int len = str.length;
        //注意偏移超过len
        offset = offset%len;
        if(offset<0) return;
        
        rotateHelper(str,len-offset,len-1);
        rotateHelper(str,0,len-offset-1);
        rotateHelper(str,0,len-1);
        
    }
    
    private void rotateHelper(char[] str,int start,int end){
        while(start<end){
            char temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }
}
```

