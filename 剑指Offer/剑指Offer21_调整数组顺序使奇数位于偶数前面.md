## &#127800; 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面 &#127800;

### &#127826; 题目

**输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。**

示例：

输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。

提示：

- 1 <= nums.length <= 50000
- 1 <= nums[i] <= 10000


### &#127826; 题解

方法一： 双指针
<details>
<summary>&#127808; View The Codes &#127808;</summary>

1. 初始化： i , j 双指针，分别指向数组 nums 左右两端；
2. 循环交换： 当 i = j 时跳出；

    - 指针 i 遇到奇数则执行 i = i+1 跳过，直到找到偶数；
    - 指针 j 遇到偶数则执行 j = j−1 跳过，直到找到奇数；
    - 交换 nums[i] 和 nums[j] 值；

3. 返回值： 返回已修改的 nums 数组。

```java
class Solution {
public int[] exchange(int[] nums) {
        int left = 0, right = nums.length - 1;
        while( left < right){
            while (left < right && (nums[left] & 1) == 1){
                left++;
            }
            while (left < right && (nums[right] & 1) == 0){
                right--;
            }
            swap(nums, left, right);
        }
        return nums;
    }

    public void swap(int[] arr, int a, int b){
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
}
```

</details>
