```java
49. 字符大小写排序
中文English
给定一个只包含字母的字符串，按照先小写字母后大写字母的顺序进行排序。

样例
样例 1:
	输入:  "abAcD"
	输出:  "acbAD"

样例 2:
	输入: "ABC"
	输出:  "ABC"
	
挑战
在原地扫描一遍完成

注意事项
小写字母或者大写字母他们之间不一定要保持在原始字符串中的相对位置。
public class Solution {
    /*
     * @param chars: The letter array you should sort by Case
     * @return: nothing
     */
    public void sortLetters(char[] chars) {
        
        if(chars==null || chars.length==0){
            return ;
        }
        
        int left = 0;
        int right = chars.length - 1;
        
        while(left < right){
            while(left<right && chars[left]>='a'&&chars[left]<='z'){
                left++;
            }
            
            while(left<right && chars[right]>='A'&&chars[right]<='Z'){
                right--;
            }
            
            if(left < right){
                char temp = chars[left];
                chars[left] = chars[right];
                chars[right]  = temp;
                
                left++;
                right--;
            }
        }
    }
}
```

