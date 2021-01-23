## &#127800; 剑指 Offer 15. 二进制中1的个数 &#127800;

### &#127826; 题目

**请实现一个函数，输入一个整数（以二进制串形式），输出该数二进制表示中 1 的个数。例如，把 9 表示成二进制是 1001，有 2 位是 1。因此，如果输入 9，则该函数输出 2。**

示例1：

输入： `00000000000000000000000000001011`

输出： `3`

解释： 输入的二进制串 `00000000000000000000000000001011` 中，共有三位为 `'1'`。

示例 2：

输入： `11111111111111111111111111111101`
输出： `31`
解释：输入的二进制串 `11111111111111111111111111111101` 中，共有 `31` 位为 `'1'`。

提示：

- 输入必须是长度为 32 的 二进制串 。



### &#127826; 题解
#### 方法一：逐位判断 &#9971;

<details>
<summary>&#127808; View The Codes &#127808;</summary>

```java
public class Solution {
    public int hammingWeight(int n) {
        int res = 0;
        while(n != 0) {
            res += n & 1;
            n >>>= 1;
        }
        return res;
    }
}
```
</details>
  
#### 方法二：迭代 &#9971;

  
<details>
<summary>&#127808; View The Codes &#127808;</summary>

```java
public class Solution {
    public int hammingWeight(int n) {
        int res = 0;
        while(n != 0) {
            res++;
            n &= n - 1;
        }
        return res;
    }
}
```
</details>

&#128640; [题解详情](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/solution/mian-shi-ti-15-er-jin-zhi-zhong-1de-ge-shu-wei-yun/ "krahets")