## &#127800; 剑指 Offer 12. 矩阵中的路径 &#127800;

### &#127826; 题目

#### 请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。
```
[["a","b","c","e"],
["s","f","c","s"],
["a","d","e","e"]]
```
#### 但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。




**示例 1：**

输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true

**示例 2：**

输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false

**提示：**

    1 <= board.length <= 200
    1 <= board[i].length <= 200


### &#127826; 题解

解题思路：
典型的矩阵搜索问题，可使用 深度优先搜索（DFS）+ 剪枝 解决。
<details>
<summary>&#127808; 滑动窗口优化 &#127808;</summary>

```java
package LeetCode_2021.Coding_2021_02_17;

public class Offer12 {
    public static void main(String[] args){
        char [][] arr = {{'a','b','c','e'}, {'s','f','c','s'},{'a','d','e','e'}};
        String str = "bfcee";
        Offer12 offer12 = new Offer12();
        System.out.println(offer12.exist(arr, str));
        System.out.println(arr.length);
    }

    // 面试题12. 矩阵中的路径（ DFS + 剪枝 ）
    public boolean exist(char[][] board, String word) {
        // String转char
        char[] words = word.toCharArray();
        // 遍历行
        for(int i = 0; i < board.length; i++) {
            // 遍历列
            for(int j = 0; j < board[0].length; j++) {
                // 开启递归
                if(dfs(board, words, i, j, 0)) return true;
            }
        }
        return false;
    }
    // 深度搜索 + 剪枝
    // board:遍历矩阵 / word:目标字符 / i: 行号 / j: 列号 / k: 当前位置
    boolean dfs(char[][] board, char[] word, int i, int j, int k) {
        // 如果i、j越界，或者当前矩阵元素已访问过
        if(i >= board.length || i < 0 || j >= board[0].length || j < 0 || board[i][j] != word[k]) return false;
        // 字符串 word 已全部匹配
        if(k == word.length - 1) return true;
        // 标记当前矩阵元素，将 board[i][j] 修改为 空字符 '' ，代表此元素已访问过，防止之后搜索时重复访问。
        // 使用空字符（Python: '' , Java/C++: '\0' ）做标记是为了防止标记字符与矩阵原有字符重复。当存在重复时，此算法会将矩阵原有字符认作标记字符，从而出现错误。
        board[i][j] = '\0';
        // 搜索下一单元格： 朝当前元素的 上、下、左、右 四个方向开启下层递归，使用 或 连接 （代表只需找到一条可行路径就直接返回，不再做后续 DFS ），并记录结果至 res 。
        boolean res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) || dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i , j - 1, k + 1);
        // 还原当前矩阵元素： 将 board[i][j] 元素还原至初始值，即 word[k] 。
        board[i][j] = word[k];
        // 返回布尔量 res ，代表是否搜索到目标字符串。
        return res;
    }
}

```
</details>
  
##### &#127826; 复杂度分析：

>M,N 分别为矩阵行列大小，K 为字符串 word 长度。
- 时间复杂度 ${O(3^KMN)}$ ： 最差情况下，需要遍历矩阵中长度为 K 字符串的所有方案，时间复杂度为 $O(3^K)$；矩阵中共有 MN 个起点，时间复杂度为 O(MN) 。
  - 方案数计算： 设字符串长度为 KKK ，搜索中每个字符有上、下、左、右四个方向可以选择，舍弃回头（上个字符）的方向，剩下 3 种选择，因此方案数的复杂度为 $O(3^K)$ 。
- 空间复杂度 O(K) ： 搜索过程中的递归深度不超过 K ，因此系统因函数调用累计使用的栈空间占用 O(K) （因为函数返回后，系统调用的栈空间会释放）。最坏情况下 K=MN ，递归深度为 MN ，此时系统栈使用 O(MN)的额外空间。