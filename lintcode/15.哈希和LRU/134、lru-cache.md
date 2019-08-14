```java
134. LRU缓存策略
中文English
为最近最少使用（LRU）缓存策略设计一个数据结构，它应该支持以下操作：获取数据和写入数据。

get(key) 获取数据：如果缓存中存在key，则获取其数据值（通常是正数），否则返回-1。
set(key, value) 写入数据：如果key还没有在缓存中，则写入其数据值。当缓存达到上限，它应该在写入新数据之前删除最近最少使用的数据用来腾出空闲位置。
最终, 你需要返回每次 get 的数据.

样例
样例 1:

输入：
LRUCache(2)
set(2, 1)
set(1, 1)
get(2)
set(4, 1)
get(1)
get(2)
输出：[1,-1,1]
解释：
cache上限为2，set(2,1)，set(1, 1)，get(2) 然后返回 1，set(4,1) 然后 delete (1,1)，因为 （1,1）最少使用，get(1) 然后返回 -1，get(2) 然后返回 1。
样例 2:

输入：
LRUCache(1)
set(2, 1)
get(2)
set(3, 2)
get(2)
get(3)
输出：[1,-1,2]
解释：
cache上限为 1，set(2,1)，get(2) 然后返回 1，set(3,2) 然后 delete (2,1)，get(2) 然后返回 -1，get(3) 然后返回 2。
public class LRUCache {
    class ListNode {
        public int key, val;
        public ListNode next;
        
        public ListNode(int key, int val) {
            this.key = key;
            this.val = val;
            this.next = null;
        }
    }
    
    private int capacity, size;
    private ListNode head, tail;
    private Map<Integer, ListNode> map;

    /*
    * @param capacity: An integer
    */
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.head = new ListNode(0,0);
        this.tail = this.head;
        this.map = new HashMap<Integer,ListNode>();
    }

    private void moveToTail(int key) {
        ListNode pre = map.get(key);
        ListNode cur = pre.next;
        
        //key已经在尾部
        if(cur==tail){
            return ;
        }
        
        pre.next = pre.next.next;
        tail.next = cur;
        if(pre.next!=null){
            map.put(pre.next.key,pre);
        }
        map.put(cur.key,tail);
        
        tail = cur;
    }
    
    /*
     * @param key: An integer
     * @return: An integer
     */
    public int get(int key) {
    
        //不在缓存中，返回-1
        if(!map.containsKey(key)){
           return -1;
        }
        //在缓存中，移动到尾部，返回val
        moveToTail(key);
       
       return tail.val;
    }
    
    /*
     * @param key: An integer
     * @param value: An integer
     * @return: nothing
     */
    public void set(int key, int value) {
        //命中缓存，移动到末尾，修改值
        if(get(key)!=-1){
            moveToTail(key);
            ListNode pre = map.get(key);
            pre.next.val = value;
            return ;
        }
        
        //没命中缓存，缓存没满,添加到尾部
        if(size<capacity){
            ListNode node = new ListNode(key,value);
            tail.next = node;
            map.put(node.key,tail);
            
            tail = node;
            size++;
            return ;
        }
        
        //没命中缓存，缓存满,删除最久未使用的，添加新的到尾部
        
        ListNode first = head.next;
        map.remove(first.key);
        
        first.key = key;
        first.val = value;
        map.put(key,head);
        
        moveToTail(key);
        
    }
}

/*public class LRUCache {
    private int capacity;
    private int size;
    private ListNode head;
    private ListNode tail;
    private Map<Integer,ListNode> map;
    
    class ListNode{
        int val;
        int key;
        ListNode next;
        
        ListNode(int key,int val){
            this.key = key;
            this.val = val;
        }
    }
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.head = new ListNode(0,0);
        this.tail = head;
        map = new HashMap<Integer,ListNode>();
    }

    
    public int get(int key) {
        //命中调整hit到最后
        if(map.containsKey(key)){
            ListNode pre = map.get(key);
            ListNode hit = pre.next;
            
            //特殊情况，命中最新的
            if(hit==tail){
                return hit.val;
            }
            
            pre.next = pre.next.next;
            hit.next = null;
            tail.next = hit;
            if(pre.next!=null){
                map.put(pre.next.key,pre);
            }
            map.put(key,tail);
            tail = hit;
            return hit.val;
        }
        //未命中，返回-1
        else{
            return -1;
        }
    }

    
    public void set(int key, int value) {
        //缓存中有key，调整hit到最后
        if(map.containsKey(key)){
            ListNode pre = map.get(key);
            ListNode hit = pre.next;
            hit.val = value;
        }
        //缓存中没有key，判断缓存是否满？未满直接添加注意size++
        else{
            if(size<capacity){
                ListNode node = new ListNode(key,value);
                tail.next = node;
                map.put(key,tail);
                node.next = null;
                tail = node;
                size++;
            }else{
                //缓存满了，删除最久未使用的，添加新的
                map.remove(head.next.key);
                head.next = head.next.next;
                if(head.next!=null){
                    map.put(head.next.key,head);
                }
                ListNode node = new ListNode(key,value);
                tail.next = node;
                map.put(key,tail);
                node.next = null;
                tail = node;
            }
        }
    }
    
}*/
```

