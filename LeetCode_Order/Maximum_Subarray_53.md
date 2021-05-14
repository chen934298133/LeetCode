## &#127800; 53. Maximum Subarray &#127800;

### &#127826; 题目


Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and ***return its sum***.

#### Example 1:

>Input: nums = `[-2,1,-3,4,-1,2,1,-5,4]`<br>
>Output: `6`<br>
>Explanation: `[4,-1,2,1]` has the largest sum = `6`.<br>

#### Example 2:

>Input: nums = `[1]`<br>
>Output: `1`<br>

#### Example 3:

>Input: nums = `[5,4,-1,7,8]`<br>
>Output: `23`<br>
 

#### Constraints:

- ${1 <= nums.length <= 3 * 10^4}$
- ${-10^5 <= nums[i] <= 10^5}$

### &#127826; 题解


<details>
<summary>&#127808; 动态规划 &#127808;</summary>

### 思路

用动态规划的思路并不难解决，比较难的是官方后文提出的用分治法求解，但由于其不是最优解法，所以先不列出来


### 步骤
1. 动态规划的是首先对数组进行遍历，当前最大连续子序列和为 sum，结果为 ans
2. 如果 sum > 0，则说明 sum 对结果有增益效果，则 sum 保留并加上当前遍历数字
3. 如果 sum <= 0，则说明 sum 对结果无增益效果，需要舍弃，则 sum 直接更新为当前遍历数字
4. 每次比较 sum 和 ans的大小，将最大值置为ans，遍历结束返回结果
  - 时间复杂度：O(n)O(n)
  
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int ans = nums[0];
        int sum = 0;
        for(int num: nums) {
            if(sum > 0) {
                sum += num;
            } else {
                sum = num;
            }
            ans = Math.max(ans, sum);
        }
        return ans;
    }
}

```
  
</details>
  
  
[参考](画手大鹏 "链接：https://leetcode-cn.com/problems/maximum-subarray/solution/hua-jie-suan-fa-53-zui-da-zi-xu-he-by-guanpengchn/")