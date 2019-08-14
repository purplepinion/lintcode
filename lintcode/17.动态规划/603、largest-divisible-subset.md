```java
public class Solution {
    /*
     * @param nums: a set of distinct positive integers
     * @return: the largest subset 
     */
    public List<Integer> largestDivisibleSubset(int[] nums) {
        
        List<Integer> list = new ArrayList<Integer>();
        
        if(nums==null || nums.length==0){
            return list;    
        }
        
        //排序很关键
        Arrays.sort(nums);
        
        int len = nums.length;
        
        int[] f = new int[len];//nums[i]是集合末尾元素的集合size最大值
        int[] pre = new int[len];//nums[i]在集合中前一个数的index
        
        //初始化
        for(int i=0;i<len;i++){
            f[i] = 1;
            pre[i] = i;
            //当nums[i]可以被nums[j]整除时，并且nums[j]结尾最大集合size大于nums[i]结尾最大集合size
            for(int j=0;j<i;j++){
                if(nums[i]%nums[j]==0 && f[i]<f[j]+1){
                    f[i] = f[j] + 1;
                    pre[i] = j;
                }
            }
        }
        
        int max = 0;
        int max_i = 0;
        //找出f[i]最大的集合
        for(int i=0;i<len;i++){
            if(f[i]>max){
                max = f[i];
                max_i = i;
            }
        }
        
        //将集合处理并且返回 注意从小到大排序
        list.add(nums[max_i]);
        while(max_i!=pre[max_i]){
            max_i = pre[max_i];
            list.add(nums[max_i]);
        }
        
        Collections.reverse(list);
        
        return list;
    }
    
    
}
```

