## &#127800; 剑指 Offer 22. 链表中倒数第k个节点 &#127800;

### &#127826; 题目

- 输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。
- 例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。


##### 示例 1:

给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.

### &#127826; 题解

<details>
<summary>&#127808; 单指针循环两次（直白思路） &#127808;</summary>

  
### 思路
- 循环第一次获取链表长度
- 循环第二次获取到链表倒数第k个节点，并返回
  
### 步骤：
1. 若只有一个节点直接返回
2. 查看链表长度
3. 获取链表正向index
4. 遍历至index,并返回
  
```java
    public ListNode getKthFromEnd(ListNode head, int k) {
        // 1. 若只有一个节点直接返回
        if (head.next == null && k == 1) {
            return head;
        }
        // 设置参照值
        int index = 1;
        ListNode tempNode = head;
        // 2. 查看链表长度
        while (tempNode.next != null) {
            tempNode = tempNode.next;
            index++;
        }
        // 3. 获取链表正向index
        int temp = index - k + 1;
        // 4. 遍历至index,并返回
        index = 1;
        while (head.next != null) {
            if (index == temp) {
                return head;
            }
            head = head.next;
            index++;
        }
        return head;
    }
```
  
</details>

<details>
<summary>&#127808; 快慢指针（循环两次） &#127808;</summary>

  
### 思路
- 快指针先行k个节点，当快指针走到最后，慢指针即为倒数第k个节点
  
### 步骤：
1. 快指针先走 k 步
2. 快指针走到头，慢指针即为倒数第k个值
  
```java
    public ListNode getKthFromEnd3(ListNode head, int k) {
        // 定义快慢指针
        ListNode fast = head, slow = head;
        // 1. 快指针先走 k 步
        for (int i = 0; i < k; i++) {
            if (fast == null) return null;
            fast = fast.next;
        }
        // 2. 快指针走到头，慢指针即为倒数第k个值
        while (slow != null) {
            fast = fast.next;
            slow = slow.next;
        }
        return slow;
    }
```
  
</details>
  
<details>
<summary>&#127808; 快慢指针（循环一次） &#127808;</summary>

  
### 思路
- 当快指针先行完成后慢指针开始移动，当快指针移动到最后时慢指针所指即为倒数第k个节点
  
### 步骤：
1. 设置一个变量判断，将快指针先行与两个指针共行放在同一个循环内
[](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/solution/mian-shi-ti-22-lian-biao-zhong-dao-shu-di-kge-j-11/ "Krahets")
2. 当快指针先行完成后慢指针开始移动，当快指针移动到最后时慢指针所指即为倒数第k个节点
  
```java
    public ListNode getKthFromEnd2(ListNode head, int k) {
        // 定义快慢指针
        ListNode slow = head, fast = head;
        //  1. 设置一个变量判断，将快指针先行与两个指针共行放在同一个循环内
        int t = 0;
        while (fast != null) {
            // 2. 当快指针先行完成后慢指针开始移动，当快指针移动到最后时慢指针所指即为倒数第k个节点
            if (t >= k) {
                slow = slow.next;
            }
            fast = fast.next;
            t++;
        }
        return slow;
    }
```
  
</details>
  