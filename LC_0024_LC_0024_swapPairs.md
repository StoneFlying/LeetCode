#### 24. 两两交换链表中的节点
    
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

 

#### 示例 1：

```
    输入：head = [1,2,3,4]
    输出：[2,1,4,3]
```


#### 解释

```
迭代交换相邻节点即可
时间复杂度:O(N)     空间复杂度:O(1)
```

```Java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode();
        dummy.next = head;
        ListNode temp = dummy;
        while (temp.next != null && temp.next.next != null) {
            ListNode node1 = temp.next;
            ListNode node2 = temp.next.next;
            temp.next = node2;
            node1.next = node2.next;
            node2.next = node1;
            temp = node1;
        }
        return dummy.next;
    }
}
```