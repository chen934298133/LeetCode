## &#127800; 剑指 Offer 24. 反转链表 &#127800;

### &#127826; 题目

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。


##### 示例 1:

输入: 1->2->3->4->5->NULL<br>
输出: 5->4->3->2->1->NULL

##### 限制：

0 <= 节点个数 <= 5000

### &#127826; 题解
[题解参考](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/solution/fan-zhuan-lian-biao-yi-dong-de-shuang-zhi-zhen-jia/ "路漫漫我不畏")
<details>
<summary>&#127808; 双指针局部反转 &#127808;</summary>
  
<![](https://files.mdnice.com/user/1562/38035d69-51e6-409d-ba40-eb42c8bf775f.png),![](https://files.mdnice.com/user/1562/91fadf88-5872-42e4-8cac-2991b3ee3eab.png),![](https://files.mdnice.com/user/1562/cd6e5121-d9fe-47f9-a697-39891acf78d6.png),![](https://files.mdnice.com/user/1562/050b93f6-c6ac-402c-8c29-dfe81551660d.png),![](https://files.mdnice.com/user/1562/f02fb3cb-2da6-486b-82f6-edad694f0940.png),![](https://files.mdnice.com/user/1562/cea80c2a-bf92-4440-aee2-69a07b6a28c3.png),![](https://files.mdnice.com/user/1562/ee86c8da-1e81-4f87-8c4e-78de49b6e1d8.png),![](https://files.mdnice.com/user/1562/a7ee4a1b-95f3-4661-98f8-b7d08442fd89.png)>
  
### 思路
- 定义两个指针： pre 和 cur ；pre 在前 cur 在后。
- 每次让 pre 的 next 指向 cur ，实现一次局部反转
- 局部反转完成之后， pre 和 cur 同时往前移动一个位置
- 循环上述过程，直至 pre 到达链表尾部

### 步骤：
1. 定义双指针，一快一慢
2. 模拟pre、cur前进
  - 获取pre的下一个节点，为pre的移动做准备
  - 局部反转，pre.next 指向 当前 cur
  - cur前进一个节点
  - pre前进一个节点
  
```java
    public ListNode reverseList(ListNode head) {
        // 1. 定义双指针，一快一慢
        ListNode cur = null, pre = head;
        // 2. 模拟pre、cur前进
        while (pre != null) {
            // a. 获取pre的下一个节点，为pre的移动做准备
            ListNode temp = pre.next;
            // b. 局部反转，pre.next 指向 当前 cur
            pre.next = cur;
            // c. cur前进一个节点
            cur = pre;
            // d. pre前进一个节点
            pre = temp;
        }
        return cur;
    }
```
  
</details>

<details>
<summary>&#127808; 双指针局部反转(单指针移动) &#127808;</summary>

<![1](https://files.mdnice.com/user/1562/1f31766c-9e99-46b0-9077-af7cb86f10df.png),![2](https://files.mdnice.com/user/1562/8f27b17b-78e6-46ed-80c3-e0405492ddb5.png),![3](https://files.mdnice.com/user/1562/e3955655-0d89-48ff-a9cb-7858b1903df7.png),![4](https://files.mdnice.com/user/1562/ef57568d-8fdb-4da2-82ea-4c50db3cbf3f.png),![5](https://files.mdnice.com/user/1562/d63932fd-eabe-4b4c-9c42-1bdf67ae20cb.png),![6](https://files.mdnice.com/user/1562/74b5ca71-7f78-4553-8ea0-9ffb02bcce61.png),![](https://files.mdnice.com/user/1562/4f07e5b5-4dcf-4bd5-adcd-3e63d5d47fcf.png)>  
  
### 思路
- 原链表的头结点就是反转之后链表的尾结点，使用 head 标记 .
- 定义指针 cur，初始化为 head .
- 每次都让 head 下一个结点的 next 指向 cur ，实现一次局部反转
- 局部反转完成之后，cur 和 head 的 next 指针同时 往前移动一个位置
- 循环上述过程，直至 cur 到达链表的最后一个结点 .


### 步骤：
- 见注释
  
  
```java
    public ListNode reverseList2(ListNode head) {
        // 原链表的头结点就是反转之后链表的尾结点，使用 head 标记 .
        if (head == null) { return null; }
        // 定义指针 cur，初始化为 head .
        ListNode cur = head;
        while (head.next != null) {
            ListNode t = head.next.next;
            // 每次都让 head 下一个结点的 next 指向 cur ，实现一次局部反转
            head.next.next = cur;
            // 局部反转完成之后，cur 和 head 的 next 指针同时 往前移动一个位置
            cur = head.next;
            head.next = t;
        }
        // 循环上述过程，直至 cur 到达链表的最后一个结点 .
        return cur;
    }
```
  
</details>
  
<details>
<summary>&#127808; 递归 &#127808;</summary>

<![](https://files.mdnice.com/user/1562/594c8a30-db33-462f-baa1-2e2c724e577e.png),![](https://files.mdnice.com/user/1562/68e70eb4-2fd7-4a31-9e84-df080d147a1c.png),![](https://files.mdnice.com/user/1562/7002b39d-e012-4109-a8b2-91c6e16e8943.png),![](https://files.mdnice.com/user/1562/371908dc-f3d4-46c0-ac93-373744bce469.png),![](https://files.mdnice.com/user/1562/96cea3c9-757e-4652-8662-a708bc4a76a6.png),![](https://files.mdnice.com/user/1562/e48eb5ec-5641-4b39-bfa0-a107bf0ffe9a.png),![](https://files.mdnice.com/user/1562/04c3396a-34a7-4700-ba80-0963dfaf17bc.png),![](https://files.mdnice.com/user/1562/defe54c0-96e9-40a3-9caf-3fd97a52df7e.png),![](https://files.mdnice.com/user/1562/c8704d02-2eef-4b6f-be9b-16a25b91a025.png),![](https://files.mdnice.com/user/1562/031049e8-337b-401d-9fa8-f6d48e744113.png),![](https://files.mdnice.com/user/1562/22b81b32-6479-4805-917d-ab80bb877f34.png),![](https://files.mdnice.com/user/1562/d6bd9d27-b052-42aa-a801-15fe25a913ff.png)>  

### 思路
- 使用递归函数，一直递归到链表的最后一个结点，该结点就是反转后的头结点，记作 retret .
- 此后，每次函数在返回的过程中，让当前结点的下一个结点的 nextnext 指针指向当前节点。
- 同时让当前结点的 nextnext 指针指向 NULLNULL ，从而实现从链表尾部开始的局部反转
- 当递归函数全部出栈后，链表反转完成。
  
### 步骤：
- 见注释
  
```java
    public ListNode reverseList1(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        // 递归至最后一个节点，开始给返回链表设值
        ListNode ret = reverseList1(head.next);
        // head节点的下一个节点指向head
        head.next.next = head;
        // head节点指向null
        head.next = null;
        // 完成局部反转
        return ret;
    }
```
  
</details>
  