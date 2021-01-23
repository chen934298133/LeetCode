## Description of the question
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 _[3,4,5,1,2]_ 为 _[1,2,3,4,5]_ 的一个旋转，该数组的最小值为1。
- Example：
```java
input: [3,4,5,1,2]
output：1
```

## [Details of the solution](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/mian-shi-ti-11-xuan-zhuan-shu-zu-de-zui-xiao-shu-3/ "LeetCode_Krahets")
如下图所示，寻找旋转数组的最小元素即为寻找 **右排序数组** 的首个元素 nums[x]，称 xxx 为 **旋转点** 。
![](https://pic.leetcode-cn.com/1599404042-JMvjtL-Picture1.png )
排序数组的查找问题首先考虑使用 **二分法** 解决，其可将 **遍历法** 的 **线性级别 _O(n)_** 时间复杂度降低至 **对数级别 _O(logn)_** 。

##算法流程
<details>
<summary>&#127808; View The Details &#127808;</summary>

  1. 初始化： 声明 i, j 双指针分别指向 nums 数组左右两端；
  2. 循环二分： 设 m = (i+j)/2 为每次二分的中点（ "/" 代表向下取整除法，因此恒有 i ≤ m < j），可分为以下三种情况：
	  1. 当 nums[m] > nums[j] 时： m 一定在 左排序数组 中，即旋转点 x 一定在 [m+1,j] 闭区间内，因此执行 i = m+1；
	  2. 当 nums[m] < nums[j]时： m 一定在 **右排序数组** 中，即旋转点 x 一定在[i,m] 闭区间内，因此执行 j = m；
	  3. 当 nums[m] = nums[j] 时： 无法判断 m 在哪个排序数组中，即无法判断旋转点 x 在 [i,m] 还是 [m+1,j] 区间中。解决方案： 执行 j = j−1 缩小判断范围，分析见下文。
  3. 返回值： 当 i = j 时跳出二分循环，并返回 旋转点的值 nums[i] 即可。
             
![](https://pic.leetcode-cn.com/1599404042-VzHrmU-Picture2.png)
![](https://pic.leetcode-cn.com/1599404042-fNXpQJ-Picture3.png)
![]()
![](https://pic.leetcode-cn.com/1599404042-qbOflt-Picture4.png) 
![](https://pic.leetcode-cn.com/1599404042-sBLuCR-Picture5.png) 
![](https://pic.leetcode-cn.com/1599404042-lYmLFN-Picture6.png) 
![](https://pic.leetcode-cn.com/1599404042-HkRBZW-Picture7.png) 
![](https://pic.leetcode-cn.com/1599404366-eOwigV-Picture8.png) 
![](https://pic.leetcode-cn.com/1599404366-ngPDoD-Picture9.png) 
![](https://pic.leetcode-cn.com/1599404438-qzDKAI-Picture10.png)
                            
</details>
  
<details>
<summary>&#127808; View The Code &#127808;</summary>

```java
class Solution {
    public int minArray(int[] numbers) {
        int i = 0, j = numbers.length - 1;
        while (i < j) {
            int m = (i + j) / 2;
            if (numbers[m] > numbers[j]) i = m + 1;
            else if (numbers[m] < numbers[j]) j = m;
            else j--;
        }
        return numbers[i];
    }
}

```
</details>
当出现 nums[m]=nums[j] 时，一定有区间 [i,m] 内所有元素相等 或 区间 [m,j] 内所有元素相等（或两者皆满足）。对于寻找此类数组的最小值问题，可直接放弃二分查找，而使用线性查找替代。


<details>
<summary>&#127808; View The Codes &#127808;</summary>

```java
  class Solution {
    public int minArray(int[] numbers) {
        int i = 0, j = numbers.length - 1;
        while (i < j) {
            int m = (i + j) / 2;
            if (numbers[m] > numbers[j]) i = m + 1;
            else if (numbers[m] < numbers[j]) j = m;
            else {
                int x = i;
                for(int k = i + 1; k < j; k++) {
                    if(numbers[k] < numbers[x]) x = k;
                }
                return numbers[x];
            }
        }
        return numbers[i];
    }
}

```
</details>

[参考Krehets大佬题解](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/mian-shi-ti-11-xuan-zhuan-shu-zu-de-zui-xiao-shu-3/ "Krahets_Code")






