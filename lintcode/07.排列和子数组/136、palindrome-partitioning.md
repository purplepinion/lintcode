```java
/*
136. 分割回文串
中文English
给定字符串 s, 需要将它分割成一些子串, 使得每个子串都是回文串.

返回所有可能的分割方案.

样例
样例 1:

输入: "a"
输出: [["a"]]
解释: 字符串里只有一个字符, 也就只有一种分割方式 (就是它本身)
样例 2:

输入: "aab"
输出: [["aa", "b"], ["a", "a", "b"]]
解释: 有两种分割的方式.
    1. 将 "aab" 分割成 "aa" 和 "b", 它们都是回文的.
    2. 将 "aab" 分割成 "a", "a" 和 "b", 它们全都是回文的.
注意事项
不同的方案之间的顺序可以是任意的.
一种分割方案中的每个子串都必须是 s 中连续的一段.
*/
public class Solution {
    /*
     * @param s: A string
     * @return: A list of lists of string
     */
    public List<List<String>> partition(String s) {
        
        List<List<String>> results = new ArrayList<>();
        if(s==null||s.length()==0){
            return results;
        }
        
        List<String> subRes = new ArrayList<>();
        
        helper(results,subRes,0,s);
        
        return results;
    }
    
    private void helper(
        List<List<String>> results,
        List<String> subRes,
        int startIndex,
        String s
        ){
        
        
        if(startIndex==s.length()){
            results.add(new ArrayList<String>(subRes));
            return;
        }
        
        for(int i=startIndex;i<s.length();++i){
            String subString = s.substring(startIndex,i+1);
            if(!isPalidrome(subString)){
                continue;
            }
            subRes.add(subString);
            helper(results,subRes,i+1,s);//notice
            subRes.remove(subRes.size()-1);
        }
    }
    
    private boolean isPalidrome(String s){
        int start = 0;
        int end = s.length()-1;
        while(start<end){
            if(s.charAt(start)!=s.charAt(end)){
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
}
```

