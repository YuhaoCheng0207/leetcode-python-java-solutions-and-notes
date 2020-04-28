```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        if head == None:
            return None
        if head.next == None:
            return head
       
        p2 = head.next
        head.next = self.swapPairs(p2.next)
        p2.next = head
        return p2
```



```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null ){
            return null ;
        }
        if (head.next == null ){
            return head;
        }
        ListNode p2 = head.next;
        head.next = this.swapPairs(p2.next);
        p2.next = head;
        return p2;
        

    }
}
```


