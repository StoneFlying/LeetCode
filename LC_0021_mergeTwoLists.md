#### 21. 合并两个有序链表
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

 

#### 示例：

```
    输入：1->2->4, 1->3->4
    输出：1->1->2->3->4->4
```

#### 解释

```
迭代，每次选择小元素构建链表
时间复杂度:O(m+n)      空间复杂度:O(1)
```

```Java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        ListNode head = new ListNode();
        ListNode tail = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                tail.next = l1;
                l1 = l1.next;
                tail = tail.next;
            } else {
                tail.next = l2;
                l2 = l2.next;
                tail = tail.next;
            }
        }
        tail.next = l1 == null ? l2 : l1;
        return head.next;
    }
}
```

#### 解释

```
递归, 每次选择较小的节点与剩下的节点进行merge操作
时间复杂度:O(m+n)   空间复杂度:O(m+n)
```

```Java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        if (l1.val < l2.val) {
            l1.next =  mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l2.next, l1);
            return l2;
        }
    }
}
```