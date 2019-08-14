```java
415. 有效回文串
中文English
给定一个字符串，判断其是否为一个回文串。只考虑字母和数字，忽略大小写。

样例
样例 1:

输入: "A man, a plan, a canal: Panama"
输出: true
解释: "amanaplanacanalpanama"
样例 2:

输入: "race a car"
输出: false
解释: "raceacar"
挑战
O(n) 时间复杂度，且不占用额外空间。

注意事项
你是否考虑过，字符串有可能是空字符串？这是面试过程中，面试官常常会问的问题。

在这个题目中，我们将空字符串判定为有效回文。
public class Solution {
    /**
     * @param s: A string
     * @return: Whether the string is a valid palindrome
     */
    public boolean isPalindrome(String s) {
        if(s==null||s.length()==0){
            return true;
        }
        
        s = s.toLowerCase();
        
        int left = 0;
        int right = s.length() - 1;
        
        while(left<right){
            while(left<s.length()&&!inRange(s.charAt(left))){
                left++;
            }
            
            if(left==s.length()){
                return true;
            }
            
            while(right>=0&&!inRange(s.charAt(right))){
                right--;
            }
            
            //wrong
            //if(s.charAt(left)==s.charAt(right)||Math.abs(s.charAt(left)-s.charAt(right))==32){
            if(s.charAt(left)==s.charAt(right)){
                left++;
                right--;
            }else{
                return false;
            }
        }
        
        return right<=left;
    }
    
    
    private boolean inRange(char c){
        if(c>='A'&&c<='Z' || c>='a'&&c<='z' || c>='0'&&c<='9'){
            return true;
        }else{
            return false;
        }
        /*return Character.isLetter(c) || Character.isDigit(c);*/
    }
}
```

