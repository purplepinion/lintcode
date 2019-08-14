```java
/*
一个由二进制矩阵表示的图，0 表示白色像素点，1 表示黑色像素点。黑色像素点是联通的，即只有一块黑色区域。像素是水平和竖直连接的，给一个黑色像素点的坐标 (x, y) ，返回囊括所有黑色像素点的矩阵的最小面积。

样例
样例 1:

输入：["0010","0110","0100"]，x=0，y=2
输出：6
解释：
矩阵左上角坐标是(0, 1), 右下角的坐标是(2, 2)
样例 2:

输入：["1110""1100""0000""0000"], x = 0, y = 1
输出：6
解释：
矩阵左上角坐标是(0,  0), 右下角坐标是(1, 3)
*/
public class Solution {
    /**
     * @param image: a binary matrix with '0' and '1'
     * @param x: the location of one of the black pixels
     * @param y: the location of one of the black pixels
     * @return: an integer
     */
    public int minArea(char[][] image, int x, int y) {
        if(image==null||image.length==0||image[0]==null||image[0].length==0) return 0;
        
        int up = searchUp(image,0,x);
        int down = searchDown(image,x,image.length-1);
        int left = searchLeft(image,0,y);
        int right = searchRight(image,y,image[0].length-1);
        
        return (down-up+1) * (right-left+1);
    }
    
    private int searchUp(char[][] image,int start,int end){
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(isEmptyRow(image,mid)){
                start = mid;
            }else{
                end = mid;
            }
        }
        
        if(isEmptyRow(image,start)){
            return end;
        }else{
            return start;
        }
        
    }
    
    private int searchDown(char[][] image,int start,int end){
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(isEmptyRow(image,mid)){
                end = mid;
            }else{
                start = mid;
            }
        }
        
        if(isEmptyRow(image,end)){
            return start;
        }else{
            return end;
        }
    }
    
    private int searchLeft(char[][] image,int start,int end){
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(isEmptyCol(image,mid)){
                start = mid;
            }else{
                end = mid;
            }
        }
        
        if(isEmptyCol(image,start)){
            return end;
        }else{
            return start;
        }
    }
    
    private int searchRight(char[][] image,int start,int end){
        while(start + 1 < end){
            int mid = start + (end - start)/2;
            if(isEmptyCol(image,mid)){
                end = mid;
            }else{
                start = mid;
            }
        }
        
        if(isEmptyCol(image,end)){
            return start;
        }else{
            return end;
        }
    }
    
    private boolean isEmptyRow(char[][] image,int row){
        for(int i=0;i<=image[0].length-1;++i){
            if(image[row][i]=='1')
                return false;
        }
        return true;
    }
    
    private boolean isEmptyCol(char[][] image,int col){
        for(int i=0;i<=image.length-1;++i){
            if(image[i][col]=='1')
                return false;
        }
        return true;
    }
}
```

