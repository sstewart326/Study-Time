### Description ([[Study Time/Coding/Algorithms/Two Pointer| Linked List Problems]])

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return _the head of the merged linked list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**Input:** list1 = [1,2,4], list2 = [1,3,4]
**Output:** [1,1,2,3,4,4]

**Example 2:**

**Input:** list1 = [], list2 = []
**Output:** []

**Example 3:**

**Input:** list1 = [], list2 = [0]
**Output:** [0]

**Constraints:**

- The number of nodes in both lists is in the range `[0, 50]`.
- `-100 <= Node.val <= 100`
- Both `list1` and `list2` are sorted in **non-decreasing** order.

### Algorithm

```
Input
	1->6
	2->4->5
Output
	1->2->3->4->5->7

step 1
=======
1->6->7
^
2->4->5
^

1 < 2 
set 1 to head (head only gets set once. it is what we return)
set 1 to curr
increment pointer

step 2
=======
1->6
   ^
2->4->5
^

2 < 6 
set curr.next to 2
set curr to curr.next

step 3
========
1->6
   ^
2->4->5
   ^

4 < 6 
set curr.next to 4
set curr to curr.next

Step 4
=========
1->6
   ^
2->4->5
      ^

5 < 6 
set curr.next to 5
set curr to curr.next

Step 5
=========
1->6
   ^
2->4->5->None
          ^

second pointer is None so set 6 to curr.next
set curr to curr.next

Step 6
=========
1->6->None
       ^
2->4->5->None
          ^

both pointers are at None so return the head

```

1. 

### Solution

```
# time complexity - O(nm) - we need to iterate over two linked lists
# space complexity - O(n) - we creating a new linked list and writing
def merge_two_lists(list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:  
  
    if not list1:  
        return list2  
    if not list2:  
        return list1  
  
    head = None  
    curr = None  
    list1_next = list1  
    list2_next = list2  
  
    if list1.val <= list2.val:  
        head = ListNode(list1.val)  
        curr = head  
        list1_next = list1.next  
    else:  
        head = ListNode(list2.val)  
        curr = head  
        list2_next = list2.next  
  
    while list1_next is not None or list2_next is not None:  
        if not list1_next:  
            curr.next = list2_next  
            list2_next = list2_next.next  
        elif not list2_next:  
            curr.next = list1_next  
            list1_next = list1_next.next  
        else:  
            if list1_next.val <= list2_next.val:  
                curr.next = list1_next  
                list1_next = list1_next.next  
            else:  
                curr.next = list2_next  
                list2_next = list2_next.next  
        curr = curr.next  
    return head
```
