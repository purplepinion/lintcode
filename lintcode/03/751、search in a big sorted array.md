```java
/*
751、search in a big sorted array.m
给定一个巨大的不知道大小的数组，通过ArrayReader.get(k)获得第k个数，查找target下标，时间复杂度O(logN)
*/



public class Solution {

    public int searchBigSortedArray(int target) {
		int index = 1;
        while(ArrayReader.get(index-1)<target){
            index = index * 2;
        }
        
        int start = 0;
        int end = index;
        
        while(start+1 < end){
            int mid = start + (end - start)/2;
            if(ArrayReader.get(mid)==target){
                end = mid;
            }else if(ArrayReader.get(mid)<target){
                start = mid;
            }else if(ArrayReader.get(mid)>target){
                end = mid;
            }
        }
        
        if(ArrayReader.get(start)==target) return start;
        if(ArrayReader.get(end)=target) return end;
        
        return -1;
    }
}
```

