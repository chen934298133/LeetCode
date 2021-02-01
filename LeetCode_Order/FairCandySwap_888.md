## &#127800; 888. 公平的糖果棒交换 &#127800;

### &#127826; 题目

**爱丽丝和鲍勃有不同大小的糖果棒：A[i] 是爱丽丝拥有的第 i 根糖果棒的大小，B[j] 是鲍勃拥有的第 j 根糖果棒的大小.**

**因为他们是朋友，所以他们想交换一根糖果棒，这样交换后，他们都有相同的糖果总量。（一个人拥有的糖果总量是他们拥有的糖果棒大小的总和。）**

**返回一个整数数组 ans，其中 ans[0] 是爱丽丝必须交换的糖果棒的大小，ans[1] 是 Bob 必须交换的糖果棒的大小。**

**如果有多个答案，你可以返回其中任何一个。保证答案存在。**

示例1：

输入：A = [1,1], B = [2,2]
输出：[1,2]

示例 2：

输入：A = [1,2], B = [2,3]
输出：[1,2]

示例 3：

输入：A = [2], B = [1,3]
输出：[2,3]

示例 4：

输入：A = [1,2,5], B = [2,4]
输出：[5,4]


### &#127826; 题解

方法一： HashSet
<details>
<summary>&#127808; View The Codes &#127808;</summary>

爱丽丝的大小为 x 的糖果棒与鲍勃的大小为 y 的糖果棒交换，则有如下等式：

sumA − x + y = sumB + x − y

化简，得：

$x = y + \frac{\textit{sumA} - \textit{sumB}}{2}$

  即对于 B 中的任意一个数 y′，只要 A 中存在一个数 x′，满足 $x' = y' + \dfrac{\textit{sumA} - \textit{sumB}}{2}$，那么 {x′,y′} 即为一组可行解。

为了快速查询 A 中是否存在某个数，我们可以先将 A 中的数字存入哈希表中。然后遍历 B 序列中的数 y′，在哈希表中查询是否有对应的 x′。


```java
class Solution {
    public int[] fairCandySwap(int[] A, int[] B) {
        int sumA = Arrays.stream(A).sum();
        int sumB = Arrays.stream(B).sum();
        int delta = (sumA - sumB) / 2;
        Set<Integer> rec = new HashSet<Integer>();
        for (int num : A) {
            rec.add(num);
        }
        int[] ans = new int[2];
        for (int y : B) {
            int x = y + delta;
            if (rec.contains(x)) {
                ans[0] = x;
                ans[1] = y;
                break;
            }
        }
        return ans;
    }
}
```
</details>
