### 思路
关键在于指针的运用，其实一共用到了3个指针，一个指针是头指针，保持不动，一个前指针，一个后指针，保持距离为k，两者同时移动，一直移动到list的结尾，然后进行链表的拆分和重新连接


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if head == None or head.next == None:
            return head
        pre = head
        l = 1
        while pre.next != None:
            pre = pre.next
            l += 1
        k = k % l
        if k == 0:
            return head
        pre = head
        end = head
        while k != 0:
            end = end.next
            k -= 1
        while end.next != None:
            pre = pre.next
            end = end.next
        cur = pre.next
        pre.next = None
        end.next = head
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
    public ListNode rotateRight(ListNode head, int k) {
        
        if (head == null){
            return null;
        }
        if (head.next == null){
            return head;
        }
        
        int length = 1;
        ListNode pre = head;
        while (pre.next != null){
            pre = pre.next;
            length += 1;
        }
        k = k % length;
        System.out.print(k);
        if (k == 0){
            
            return head;
        }
        ListNode end = head;
        pre = head;
        while (k != 0){
            end = end.next;
            k -= 1;
        }
        while (end.next != null){
            pre = pre.next;
            end = end.next;
        }
        end.next = head;
        ListNode cur = pre.next;
        pre.next = null;
        return cur;
    }
}


```
