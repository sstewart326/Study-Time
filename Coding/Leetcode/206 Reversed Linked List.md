
### Description

Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [5,4,3,2,1]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

**Input:** head = [1,2]
**Output:** [2,1]

**Example 3:**

**Input:** head = []
**Output:** []

**Constraints:**

- The number of nodes in the list is the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

### Algorithm [[Linked List]]

1. create a new var to track the reverse and set it to None since None will be the last element
2. iterate over our list. At each iteration we need to
	1. first track `next`. This will be the following items that still need to be processed
	2. the the current next to prev (prev is None for the first iteration)
	3. Now update the vars that are necessary for the next iteration
		1. set prev = head
		2. and head = next
3. return prev at the end since at the end of the iterations, head will be None after a next

### Solution

```
class Solution:  
  
    # create a new var to track the reverse  
    # that new var needs to start at None    # for each iteration, point the curr node to the prev (prev is None at the beginning)    # ensure prev is present for the next iteration        # runtime - O(n) where n is the number of nodes  
    # space - O(1) we are just tracking prev and head    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:  
        if not head:  
            return head  
  
        # start of our new linked list  
        prev = None  
  
        while head:  
            # track the next iteration before we update head.next for the reversal process  
            next = head.next  
            # set the next to the previous node to reverse paths  
            head.next = prev  
              
            # set prev to the current for the next iteration  
            prev = head  
            # set the curr to the next for the next iteration  
            head = next  
  
        return prev
```
