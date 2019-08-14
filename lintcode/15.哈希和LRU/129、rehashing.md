```java
129. 重哈希
中文English
哈希表容量的大小在一开始是不确定的。如果哈希表存储的元素太多（如超过容量的十分之一），我们应该将哈希表容量扩大一倍，并将所有的哈希值重新安排。假设你有如下一哈希表：

size=3, capacity=4

[null, 21, 14, null]
       ↓    ↓
       9   null
       ↓
      null
哈希函数为：

int hashcode(int key, int capacity) {
    return key % capacity;
}
这里有三个数字9，14，21，其中21和9共享同一个位置因为它们有相同的哈希值1(21 % 4 = 9 % 4 = 1)。我们将它们存储在同一个链表中。

重建哈希表，将容量扩大一倍，我们将会得到：

size=3, capacity=8

index:   0    1    2    3     4    5    6   7
hash : [null, 9, null, null, null, 21, 14, null]
给定一个哈希表，返回重哈希后的哈希表。

样例
样例 1

输入 : [null, 21->9->null, 14->null, null]
输出 : [null, 9->null, null, null, null, 21->null, 14->null, null]
注意事项
哈希表中负整数的下标位置可以通过下列方式计算：

C++/Java：如果你直接计算-4 % 3，你会得到-1，你可以应用函数：a % b = (a % b + b) % b得到一个非负整数。
Python：你可以直接用-1 % 3，你可以自动得到2。/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */    
    public ListNode[] rehashing(ListNode[] hashTable) {
        int capacity = hashTable.length*2;
        ListNode[] newHashTable = new ListNode[capacity];
        for(int i=0;i<capacity;i++){
            newHashTable[i] = new ListNode(0);
        }
        
        for(int i=0;i<hashTable.length;i++){
            ListNode curNode = hashTable[i];
            
            while(curNode!=null){
                hangNode(newHashTable[hashCode(curNode.val,capacity)],new ListNode(curNode.val));
                curNode = curNode.next;
            }
        }
        for(int i=0;i<capacity;i++){
            newHashTable[i] = newHashTable[i].next;
        }
        return newHashTable;
    }
    
    private int hashCode(int key,int capacity){
        return (key % capacity + capacity) % capacity;
    }
    private void hangNode(ListNode dummy,ListNode node){
        while(dummy.next!=null){
            dummy = dummy.next;
        }
        node.next = dummy.next;
        dummy.next = node;
    }
};

```

