```java
4. 丑数 II
中文English
设计一个算法，找出只含素因子2，3，5 的第 n 小的数。

符合条件的数如：1, 2, 3, 4, 5, 6, 8, 9, 10, 12...

样例
样例 1：

输入：9
输出：10
样例 2：

输入：1
输出：1
挑战
要求时间复杂度为 O(nlogn) 或者 O(n)。

注意事项
我们可以认为 1 也是一个丑数。
public class Solution {
    /**
     *优先队列或者堆维护生成的最小值，HashSet去重
    */
    public int nthUglyNumber(int n) {
        
        Queue<Long> queue = new PriorityQueue<Long>();
        Set<Long>set = new HashSet<Long>();
        
        Long[] factors = new Long[3];
        factors[0] = 2L;
        factors[1] = 3L;
        factors[2] = 5L;
        
        
        for(int i=0;i<3;i++){
            queue.add(factors[i]);
            set.add(factors[i]);
        }
        
        //n==1时，返回1
        Long minNum = 1L; 
        
        for(int i=1;i<n;i++){
            minNum = queue.poll();
            for(int j=0;j<3;j++){
                if(!set.contains(minNum*factors[j])){
                    queue.add(minNum*factors[j]);
                    set.add(minNum*factors[j]);
                }
            }
        }
        
        return minNum.intValue();
    }
}
```

