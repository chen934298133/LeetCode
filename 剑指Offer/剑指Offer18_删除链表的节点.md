## &#127800; 剑指 Offer 18. 删除链表的节点 &#127800;

### &#127826; 题目

- 给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

- 返回删除后的链表的头节点。

- 注意：此题对比原题有改动

##### 示例 1:

输入: `head = [4,5,1,9], val = 5`<br>
输出: `[4,1,9]`<br>
解释: `给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.`
##### 示例 2:

输入: `head = [4,5,1,9], val = 1`<br>
输出: `[4,5,9]`<br>
解释: `给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.`

#### Constraints:

- 题目保证链表中节点的值互不相同
- 若使用 C 或 C++ 语言，你不需要 free 或 delete 被删除的节点

### &#127826; 题解


<details>
<summary>&#127808; 单指针（直白思路） &#127808;</summary>

  
### 思路
- 循环定位下一个节点是要删除的节点 -> 删除
  
### 步骤：
1.若第一个节点的val就等于val，直接返回
2.若此节点后面有节点且后面的节点的val！=val就进入遍历，想后移位
3.定位到要删除节点是下一个节点后跳出遍历，然后删除节点
  
```java
    public ListNode deleteNode(ListNode head, int val) {
        ListNode result = head;
        // 1.若第一个节点的val就等于val，直接返回
        if (head.val == val) {
            return head.next;
        }
        // 2.若此节点后面有节点且后面的节点的val！=val就向后移位
        while (head.next != null && head.next.val != val) {
            head = head.next;
        }
        // 定位到要删除节点是下一个节点
        // 3.删除节点
        if (head.next != null) {
            head.next = head.next.next;
        }
        return result;
    }
```
  
</details>

<details>
<summary>&#127808; 双指针（与单指针大同小异） &#127808;</summary>

  
### 思路
- 循环定位下一个节点是要删除的节点 -> 删除
  
### 步骤：
1.若第一个节点的val就等于val，直接返回
2.若下一个节点不为空，且下一个结点的val != val 就进入遍历
3.定位到要删除节点是下一个节点后跳出遍历，然后删除节点
  
```java
    public ListNode deleteNode2(ListNode head, int val) {
        //  若第一个节点的val就等于val，直接返回
        if (head.val == val) return head.next;
        //  定义双指针
        ListNode pre = head, cur = head.next;
        // 1. 若下一个节点不为空，且下一个结点的val != val 就进入遍历
        while (cur != null && cur.val != val) {
            // 更新节点位置
            pre = cur;
            cur = cur.next;
        }
        // 2. 定位到要删除节点是下一个节点
        // 删除节点
        if (cur != null) pre.next = cur.next;
        return head;
    }
```
  
</details>
  