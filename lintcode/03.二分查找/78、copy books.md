```java
/*
437. 书籍复印
中文English
给定 n 本书, 第 i 本书的页数为 pages[i]. 现在有 k 个人来复印这些书籍, 而每个人只能复印编号连续的一段的书, 比如一个人可以复印 pages[0], pages[1], pages[2], 但是不可以只复印 pages[0], pages[2], pages[3] 而不复印 pages[1].

所有人复印的速度是一样的, 复印一页需要花费一分钟, 并且所有人同时开始复印. 怎样分配这 k 个人的任务, 使得这 n 本书能够被尽快复印完?

返回完成复印任务最少需要的分钟数.

样例
样例 1:

输入: pages = [3, 2, 4], k = 2
输出: 5
解释: 第一个人复印前两本书, 耗时 5 分钟. 第二个人复印第三本书, 耗时 4 分钟.
样例 2:

输入: pages = [3, 2, 4], k = 3
输出: 4
解释: 三个人各复印一本书.
挑战
时间复杂度 O(nk)
*/
public class Solution {
    /**
     * @param pages: an array of integers
     * @param k: An integer
     * @return: an integer
     */
    public int copyBooks(int[] pages, int k) {
        int l = 0;
        int r = Integer.MAX_VALUE;
        //二分法查找最少完成时间
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (check(pages, mid, k)) {
                r = mid;
            } else {
                l = mid;
            }
        }

        if (check(pages, l, k)) {
            return l;
        }
        return r;
    }

    private boolean check(int[] pages, int limit, int k) {
        //查询k个人在limit时间内可以复印完这些书么
        int num = 0;
        int left = 0;
        for (int item : pages) {
            //若单本书时间超过limit返回false
            if (item > limit) {
                return false;
            }
            //前一个人超过limit时间换下一个人
            if (item > left) {
                //人数++
                num++;
                //这个人时间重置为limit
                left = limit;
            }
            //复印一本书，这个人时间减少limit
            left -= item;
        }
        //所需人数是否少于或者等于k！！
        return num <= k;
    }
}
public class Solution {
    /**
     * @param pages: an array of integers
     * @param k: An integer
     * @return: an integer
     */
    public int copyBooks(int[] pages, int k) {
        if(pages==null||pages.length==0||k<1) return 0;
        
        int start = 0;
        int end = Integer.MAX_VALUE;
        
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            
            if(check(pages,mid,k)){
                end = mid;
            }else{
                start = mid;
            }
        }
        
        if(check(pages,start,k)) return start;
        
        return end;
    }
    
    private boolean check(int[] pages,int limit,int k){
        int num = 0;
        int left = 0;
        
        for(int page:pages){
            
            if(page>limit) return false;
            
            if(page>left){
                num++;
                left = limit;
            }
            
            left = left - page;
        }
        
        return num<=k;
    }
}
```

