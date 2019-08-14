```java
545. 前K大数 II
中文English
实现一个数据结构，提供下面两个接口
1.add(number) 添加一个元素
2.topk() 返回前K大的数

样例
样例1

输入: 
s = new Solution(3);
s.add(3)
s.add(10)
s.topk()
s.add(1000)
s.add(-99)
s.topk()
s.add(4)
s.topk()
s.add(100)
s.topk()
		
输出: 
[10, 3]
[1000, 10, 3]
[1000, 10, 4]
[1000, 100, 10]

解释:
s = new Solution(3);
>> 生成了一个新的数据结构, 并且 k = 3.
s.add(3)
s.add(10)
s.topk()
>> 返回 [10, 3]
s.add(1000)
s.add(-99)
s.topk()
>> 返回 [1000, 10, 3]
s.add(4)
s.topk()
>> 返回 [1000, 10, 4]
s.add(100)
s.topk()
>> 返回 [1000, 100, 10]
样例2

输入: 
s = new Solution(1);
s.add(3)
s.add(10)
s.topk()
s.topk()

输出: 
[10]
[10]

解释:
s = new Solution(1);
>> 生成了一个新的数据结构, 并且 k = 1.
s.add(3)
s.add(10)
s.topk()
>> 返回 [10]
s.topk()
>> 返回 [10]

public class Solution {
    //space O(k)
    private int size;
    private Queue<Integer> minHeap;
    
    //time O(1)
    public Solution(int k) {
        this.size = k;
        minHeap = new PriorityQueue<Integer>();
        
    }

    //time O(logN) * N
    public void add(int num) {
        if(minHeap.size()<size){
            minHeap.offer(num);
            return ;
        }
        
        if(num>minHeap.peek()){
            minHeap.poll();
            minHeap.offer(num);
        }
        
    }

    //time O(NlogN)
    public List<Integer> topk() {
        List<Integer> list = new ArrayList<Integer>();
        
        Iterator it = minHeap.iterator();
        
        while(it.hasNext()){
            list.add((Integer)it.next());
        }
        
        Collections.sort(list,Collections.reverseOrder());
        
        return list;
    }
}
```

