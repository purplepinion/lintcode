```java
public class Solution {
    
    public int BASE = 1000000;
    /*
     * @param source: A source string
     * @param target: A target string
     * @return: An integer as index
     */
    /*
    实现时间复杂度为 O(n + m)的方法 strStr。
    strStr 返回目标字符串在源字符串中第一次出现的第一个字符的位置. 目标字串的长度为 m , 源字串的长度为 如果目标字串不在源字串中则返回 -1
    */
    public int strStr2(String source, String target) {
        if(source==null||target==null) return -1;
        
        int m = target.length();
        if(m==0) return 0;
        
        //31^m
        int power = 1;
        for(int i=0;i<m;++i){
            power = (power * 31) % BASE;
        }
        
        int targetCode = 0;
        for(int i=0;i<m;++i){
            targetCode = (targetCode*31 + target.charAt(i))%BASE;
        }
        
        int hashCode = 0;
        for(int i=0;i<source.length();++i){
            //abc+d
            hashCode = (hashCode*31 + source.charAt(i))%BASE;
            
            //小于target长度时不用减去前面的hashcode
            if(i<m){
                continue;
            }
            
            //abcd-a
            if(i>=m){
                hashCode = hashCode - (source.charAt(i-m) * power)%BASE;
                //可能产生负溢出，加上BASE变为正数
                if(hashCode<0){
                    hashCode = hashCode + BASE;
                }
            }
            //双重检查
            if(hashCode==targetCode){
                if(source.substring(i-m+1,i+1).equals(target)){
                    return i-m+1;
                }
            }
        }
        return -1;
    }
}
```

