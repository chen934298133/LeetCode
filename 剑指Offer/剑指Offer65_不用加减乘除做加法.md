## &#127800; 剑指 Offer 65. 不用加减乘除做加法 &#127800;

### &#127826; 题目

**写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。**

示例：

输入: a = 1, b = 1
输出: 2

提示：

- a, b 均可能是负数或 0
- 结果不会溢出 32 位整数


### &#127826; 题解

方法一： 二进制位运算
<details>
<summary>&#127808; View The Codes &#127808;</summary>

> 大佬画的位运算流程
> ![](https://pic.leetcode-cn.com/56d56524d8d2b1318f78e209fffe0e266f97631178f6bfd627db85fcd2503205-Picture1.png)
  
观察发现，**无进位和** 与 **异或运算** 规律相同，**进位** 和 **与运算** 规律相同（并需左移一位）。因此，无进位和 n 与进位 c 的计算公式如下；

$$\begin{cases} n = a \oplus b & 非进位和：异或运算 \\ c = a \& b << 1 & 进位：与运算 + 左移一位 \end{cases}$$

（和 s ）=（非进位和 n ）+（进位 c ）。即可将 s=a+b 转化为：

$$s=a+b ⇒ s=n+c$$

循环求 n 和 c ，直至进位 c=0 ；此时 s=n ，返回 n 即可。

> 在计算机系统中，数值一律用 补码 来表示和存储。补码的优势： 加法、减法可以统一处理（CPU只有加法器）。因此，以上方法 同时适用于正数和负数的加法 。
  
  
![](https://pic.leetcode-cn.com/d8f7b12858886ecc73165f0f4b07849e264bdc3c662835d845d14ccbff42a28f-Picture2.png)
![](https://pic.leetcode-cn.com/7b793038c4ef2263888c8caf763328db667438959674a89003fed68c56c5dbac-Picture3.png)
![](https://pic.leetcode-cn.com/b67b0ebd864c44a0240b4933eed7247705650bd6f353f541432db023b98a438f-Picture4.png)
![](https://pic.leetcode-cn.com/d07919f47d9da7550711882da75c9701c0a49bdbee55e7f8f712fafdb84b9464-Picture5.png)
![](https://pic.leetcode-cn.com/bf214dcad3e25f92477ab46c7904f5104942ec934732a439e82c394529f12f54-Picture6.png)

```java
class Solution {
    public int add(int a, int b) {
        while(b != 0) { // 当进位为 0 时跳出
            int c = (a & b) << 1;  // c = 进位
            a ^= b; // a = 非进位和
            b = c; // b = 进位
        }
        return a;
    }
}

```
[krahets题解](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/solution/mian-shi-ti-65-bu-yong-jia-jian-cheng-chu-zuo-ji-7/ "krahets")
</details>
