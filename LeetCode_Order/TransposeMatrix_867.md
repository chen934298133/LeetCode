## &#127800; 867. Transpose Matrix (转置矩阵) &#127800;

### &#127826; 题目

#### Given a 2D integer array `matrix`, return the transpose of `matrix`.The `transpose` of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.

#### 给你一个二维整数数组 `matrix`， 返回 `matrix` 的 转置矩阵 。矩阵的 `转置` 是指将矩阵的主对角线翻转，交换矩阵的行索引与列索引。

![](http://lc-dDwI9S44.cn-n1.lcfile.com/10c36d076ae9e19fab3b.png/Leetcode_867.png)

**Example 1:**<br>

Input: `matrix = [[1,2,3],[4,5,6],[7,8,9]]`<br>
Output: `[[1,4,7],[2,5,8],[3,6,9]]`<br>

**Example 2:**<br>

Input: `matrix = [[1,2,3],[4,5,6]]`<br>
Output: `[[1,4],[2,5],[3,6]]`<br>


**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 1000`
- `1 <= m * n <= 105`
- `-109 <= matrix[i][j] <= 109`

### &#127826; 题解

解题思路：
如果矩阵 `matrix` 为 `m` 行 `n` 列，则转置后的矩阵 `matrix` 为 `n` 行 `m` 列，且对任意 `0≤i<m `和 `0≤j<n`，都有 ${\textit{matrix}^\text{T}[j][i]=\textit{matrix}[i][j]}$。

创建一个 nnn 行 mmm 列的新矩阵，根据转置的规则对新矩阵中的每个元素赋值，则新矩阵为转置后的矩阵。

<details>
<summary>&#127808; 转置 &#127808;</summary>

```java
class Solution {
    public int[][] transpose(int[][] matrix) {
        int m = matrix.length, n = matrix[0].length;
        int[][] transposed = new int[n][m];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                transposed[j][i] = matrix[i][j];
            }
        }
        return transposed;
    }
}

```
</details>
  
##### &#127826; 复杂度分析：

- 时间复杂度：`O(mn)`，其中 `m` 和 `n` 分别是矩阵 `matrix` 的行数和列数。需要遍历整个矩阵，并对转置后的矩阵进行赋值操作。

- 空间复杂度：`O(1)`。除了返回值以外，额外使用的空间为常数。