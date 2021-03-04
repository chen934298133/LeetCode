## &#127800; 剑指 Offer 29. 顺时针打印矩阵 &#127800;

### &#127826; 1 题目

#### 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。


**Example 1:**<br>

输入：`matrix = [[1,2,3],[4,5,6],[7,8,9]]`<br>
输出：`[1,2,3,6,9,8,7,4,5]`<br>

**Example 2:**<br>

输入：`matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]`<br>
输出：`[1,2,3,4,8,12,11,10,9,5,6,7]`<br>

**Constraints:**

- `0 <= matrix.length <= 100`
- `0 <= matrix[i].length <= 100`

### &#127826; 2 题解

#### 2.1 解题思路：

>根据题目示例 matrix = [[1,2,3],[4,5,6],[7,8,9]] 的对应输出 [1,2,3,6,9,8,7,4,5] 可以发现，顺时针打印矩阵的顺序是 “从左向右、从上向下、从右向左、从下向上” 循环。

- 因此，考虑设定矩阵的“左、上、右、下”四个边界，模拟以上矩阵遍历顺序。

![](http://lc-dDwI9S44.cn-n1.lcfile.com/d0ceba51ac36411573c0.png/Offer29_1.png)


#### 2.2 算法流程：
1. 空值处理: 当`matrix`为空时，直接返回空列表
2. 初始化边界: 矩阵左右上下四个边界l, r，t, b, 以及用于打印结果列表的`res`
3. 循环打印 “左->右、上->下、右->左、下->上”，四个方向循环
  - 根据边界打印，即把元素按顺序添加至列表`res`的尾部；
  - 边界向内缩1（表示已经被打印）
  - 判断是否打印完毕（边界是否相遇），若打印完毕则跳出
4. 返回`res`

<details>
<summary>&#127808; 转置 &#127808;</summary>

```java
package LeetCode_2021.Coding_2021_03_03;

import java.util.Arrays;

public class Offer29 {

    public static void main(String[] args){
        Offer29 o = new Offer29();
        int[][] matrix = {{1,2,3},{4,5,6},{7,8,9}};
        System.out.println(Arrays.toString(o.spiralOrder(matrix)));     // [1,2,3,6,9,8,7,4,5]
    }

    public int[] spiralOrder(int[][] matrix) {
        // 1. 空值处理： 当 matrix 为空时，直接返回空列表 [] 即可。
        if(matrix.length == 0) return new int[0];
        // 2. 初始化边界: 矩阵上下左右四个边界t, b, l, r
        int l = 0, r = matrix[0].length - 1, t = 0, b = matrix.length - 1, x = 0;
        //    以及初始化用于打印结果列表的`res`
        int[] res = new int[(r + 1) * (b + 1)];
        // 3. 循环打印 “左->右、上->下、右->左、下->上”，四个方向循环
        while(true) {
            for(int i = l; i <= r; i++) res[x++] = matrix[t][i]; // left to right.
            // 上缩: 边界+1
            if(++t > b) break;
            
            for(int i = t; i <= b; i++) res[x++] = matrix[i][r]; // top to bottom.
            // 右缩: 边界-1
            if(l > --r) break;
            
            for(int i = r; i >= l; i--) res[x++] = matrix[b][i]; // right to left.
            // 下缩: 边界+1
            if(t > --b) break;
            
            for(int i = b; i >= t; i--) res[x++] = matrix[i][l]; // bottom to top.
            // 左缩: 边界+1
            if(++l > r) break;
        }
        return res;
    }

}


```
</details>
  
####  2.3 复杂度分析：

- 时间复杂度：`O(mn)`，mn分别为矩阵行数和列数。

- 空间复杂度：`O(1)`。边界上下左右使用常数大小的额外空间。