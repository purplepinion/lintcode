```java
public class Solution {
    /**
     * 
     * @param key: A string you should hash
     * @param HASH_SIZE: An integer
     * @return: An integer
     */
    /*
    在数据结构中，哈希函数是用来将一个字符串（或任何其他类型）转化为小于哈希表大小且大于等于零的整数。一个好的哈希函数可以尽可能少地产生冲突。一种广泛使用的哈希函数算法是使用数值33，假设任何字符串都是基于33的一个大整数，比如：
    
    hashcode("abcd") = (ascii(a) * 333 + ascii(b) * 332 + ascii(c) *33 + ascii(d)) % HASH_SIZE 
    
                                  = (97* 333 + 98 * 332 + 99 * 33 +100) % HASH_SIZE
    
                                  = 3595978 % HASH_SIZE
    
    其中HASH_SIZE表示哈希表的大小(可以假设一个哈希表就是一个索引0 ~ HASH_SIZE-1的数组)。
    
    给出一个字符串作为key和一个哈希表的大小，返回这个字符串的哈希值。
    */
    public int hashCode(char[] key, int HASH_SIZE) {
        long ans = 0;
        for(int i=0;i<key.length;i++){
            ans = (ans*33 + (int)key[i])%HASH_SIZE;
        }
        return (int)ans;
    }
}
```

对多项式进行了处理，

$$
hashCode=((ai+b)∗i\%H+c)∗i\%H)...)+dhashCode=((ai+b)∗i\%H+c)∗i\%H)...)+d
$$
这样看比较不容易懂，举个例子，下边两个多项式是等价的：

$$
ai4+bi3+c2+d=(((ai+b)∗i+c)∗i)+dai4+bi3+c2+d=(((ai+b)∗i+c)∗i)+d
$$

然后取余数
$$
(ai4+bi3+c2+d)\%H=((((ai+b)∗i+c)∗i)+d)\%H(ai4+bi3+c2+d)\%H=((((ai+b)∗i+c)∗i)+d)\%H
$$

为了使右边多项式每次计算都能够保证不越界，变形为：
$$
((((ai+b)∗i+c)∗i)+d)\%H=((((ai+b)∗i\%H+c)∗i\%H)+d)\%H((((ai+b)∗i+c)∗i)+d)\%H=((((ai+b)∗i\%H+c)∗i\%H)+d)\%H
$$

在每一次计算后都取余，然后和传给下一次计算做累加处理。这样就能保证每次计算后的值都能够保持在一个较小的数

