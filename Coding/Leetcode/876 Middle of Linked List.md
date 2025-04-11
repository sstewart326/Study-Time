### Description

Given the `head` of a singly linked list, return _the middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [3,4,5]
**Explanation:** The middle node of the list is node 3.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

**Input:** head = [1,2,3,4,5,6]
**Output:** [4,5,6]
**Explanation:** Since the list has two middle nodes with values 3 and 4, we return the second one.

**Constraints:**

- The number of nodes in the list is in the range `[1, 100]`.
- `1 <= Node.val <= 100`

### Algorithm ([[Linked List]] - [[Study Time/Coding/Algorithms/Two Pointer|Two Pointer]])

### Solution

```
#  
# 1->2->3->4->None             1->2->3->4->5->None  
# ^                            ^  
# 1->2->3->4->None             1->2->3->4->5->None  
#    L  R                         L  R  
# 1->2->3->4->None             1->2->3->4->5->None  
#       L      R                     L     R  
# right is none, return L      right.next is none, return L  
  
# time - O(n/2) / O(n) where n is the number of nodes  
# space - O(1) just keeping track of the left and right  
class Solution:  
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:  
        if not head:  
            return head  
        left = head  
        right = head  
  
        while right and right.next:  
            left = left.next  
            right = right.next.next  
  
        return left
```

