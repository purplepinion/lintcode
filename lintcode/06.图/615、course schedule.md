```java
/*
615. 课程表
中文English
现在你总共有 n 门课需要选，记为 0 到 n - 1.
一些课程在修之前需要先修另外的一些课程，比如要学习课程 0 你需要先学习课程 1 ，表示为[0,1]
给定n门课以及他们的先决条件，判断是否可能完成所有课程？

样例
例1:

输入: n = 2, prerequisites = [[1,0]] 
输出: true
例2:

输入: n = 2, prerequisites = [[1,0],[0,1]] 
输出: false

转化为求有向图的拓扑排序，
*/
public class Solution {
    /*
     * @param numCourses: a total of n courses
     * @param prerequisites: a list of prerequisite pairs
     * @return: true if can finish all courses or false
     */
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        //存放每个vertex的邻接点
        Map<Integer,ArrayList<Integer>> edges = new HashMap<Integer,ArrayList<Integer>>();
        //存放每个vertex入度
        int[] indegree = new int[numCourses];
        //初始化
        for(int i=0;i<numCourses;++i){
            indegree[i]=0;
            edges.put(i,new ArrayList<Integer>());
        }
        //遍历输入数据，获得每个vertex入度和邻接点
        for(int i=0;i<prerequisites.length;++i){
            indegree[prerequisites[i][0]]++;
            edges.get(prerequisites[i][1]).add(prerequisites[i][0]);
        }
        //bfs 若课程数量等于最终入度为0的点则可以完成所有的课程
        Queue queue = new LinkedList();
        for(int i=0;i<numCourses;++i){
            if(indegree[i]==0){
                queue.offer(i);
            }
        }
        
        int count = 0;
        
        while(!queue.isEmpty()){
            //取出入度为0的课程，count++
            int curCourse = (int) queue.poll();
            count++;
            
            for(Integer neighbor:edges.get(curCourse)){
                //neighbor入度-- neighbor为0则添加到队列
                indegree[neighbor]--;
                if(indegree[neighbor]==0){
                    queue.offer(neighbor);
                }
            }
        }
        
        return count == numCourses;
    }
}
```

