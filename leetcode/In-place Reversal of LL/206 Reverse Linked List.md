### 思路（迭代法）
三个指针，1个指向之前的node，一个指向当前node，一个指向下一个node
之前的node是用来被指向的
当前的node指向之前的node
下一个node用来存储之后的位置，防止丢失后面的node
每次改变指向后，集体后移，循环，直到下一个node为None


```python

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if head == None :
            return head
        pre = None
        cur = head
        after = cur.next
        cur.next = pre
        while after != None:
            pre = cur
            cur = after
            after = after.next
            cur.next = pre
        return cur


```

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null) return null;
        ListNode pre = null;
        ListNode after = head.next;
        head.next = pre;
        while (after != null){
            pre = head;
            head = after;
            after = after.next;
            head.next = pre;
        }
        return head;
    }
}


```

### 思路（递归法）
关键在于两个输入参数，可能不是很完美
base line：如果当前节点cur下一个节点为none，则结束，返回该结点指针，该节点指向之前的pre指针
normal case：当前节点指向之前的pre指针，当前节点作为pre，当前节点的下一个节点作为当前节点cur，递归。

```python

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if head == None or head.next == None:
            return head
        cur = self.reverse(head, head.next)
        head.next = None
        return cur
    def reverse(self, cur: ListNode, after: ListNode):
        if after.next == None:
            after.next = cur
            return after
        else:
            res = self.reverse(after, after.next)
            after.next = cur
            return res


```