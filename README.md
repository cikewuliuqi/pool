566. Reshape the Matrix
567. In MATLAB, there is a very useful function called 'reshape', which can reshape a matrix into a new one with different size but keep its original data.

You're given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively.

The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

Example 1:
Input: 
nums = #  #
[[1,2],
 [3,4]]
r = 1, c = 4
Output: 
[[1,2,3,4]]
Explanation:
The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
Example 2:
Input: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4
Output: 
[[1,2],
 [3,4]]
Explanation:
There is no way to reshape a 2 * 2 matrix to a 2 * 4 matrix. So output the original matrix.

Note:
The height and width of the given matrix is in range [1, 100].
The given r and c are all positive.


简单介绍矩阵
We can implement a matrix using two dimensional array in Java. The element at row “r” and column “c” can be accessed using index “array[r]“.
二位数组创建一个矩阵

Since we are using two-dimensional arrays to create a matrix, we can easily perform various operations on its elements. In this tutorial, we will learn how to create a matrix from user input. Then we will add, subtract, and multiply two matrices and print the result matrix on the console.
对元素进行操作特别方便

int[][] first = new int[row][column];
int[][] second = new int[row][column];
创建一个几行几列的矩阵

动态初始化与静态初始化
遍历的方式为三种：普通for，加强for与arrays.deepToString()

第一反应：遍历矩阵，然后按照给出的格式输出
//经典版本
public int[][] matrixReshape(int[][] nums, int r, int c) {
    int n = nums.length, m = nums[0].length;    //calculate rows and columns 这里N是多少行 M是多少列
    if (r*c != n*m) return nums;			//equals the score of the value
    int[][] res = new int[r][c];				//create matrix
    for (int i=0;i<r*c;i++) 					//reverse 遍历次数为所有值的总数
        res[i/c][i%c] = nums[i/m][i%m];			//assignment 最关键的部分  用i除以各自的列 先取整 在取余
    return res;             //返回res
}

//繁琐版本
 yours is so concise... learned a lot
public int[][] matrixReshape(int[][] nums, int r, int c) {
        if(nums == null || nums.length == 0)
            return null;
        
        int row_nums = nums.length;
        int col_nums = nums[0].length;
        
        if(row_nums * col_nums != r * c)
            return nums;
        
        int[][] res = new int[r][c];
        List<Integer> list = new ArrayList<>();
        //新建一个list，接收所有的value。
        for(int[] row : nums)
        {
            for(int col : row)
            {
                list.add(col);
            }
        }
        //将value一次赋值
        for(int i = 0; i < r; i++)
        {
            for(int j = 0; j < c; j++)//c指的是列数
            {
                int index = i * c + j;//索引值为行 列 以及c求得  第几行第几个  行乘以最大列加上现在的列数
                res[i][j] = list.get(index);
            }
        }
        return res;
    }
//可能版本（和第一个版本一模一样）
We can use matrix[index / width][index % width] for both the input and the output matrix.
public int[][] matrixReshape(int[][] nums, int r, int c) {
    int m = nums.length, n = nums[0].length;
    if (r * c != m * n)
        return nums;
    int[][] reshaped = new int[r][c];
    for (int i = 0; i < r * c; i++)
        reshaped[i/c][i%c] = nums[i/n][i%n];
    return reshaped;
}
//简单容易想的版本
public class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int m = nums.length, n = nums[0].length;
        if (m * n != r * c) return nums;
        //两层循环  赋值。立马
        int[][] result = new int[r][c];
        int row = 0, col = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                result[row][col] = nums[i][j];
//索引递增。当行到达最大的位置，回到0,且把列加1 继续刚才的操作
                col++;
                if (col == c) {
                    col = 0;
                    row++;
                }
            }
        }
//最后返回出去
        return result;
    }
}
最后总结：这个问题一共有三种解法，每次都比之前更加简洁，第一种思路。用一个list集合装所有元素，然后利用索引值依次赋值，两个for，两次遍历第二种依次循环。每次循环结束，立马赋值。此时需要注意如何一一对应 第三种方法有技巧性 只需要一个for就可以了，利用了取整和取余 特别有意思
