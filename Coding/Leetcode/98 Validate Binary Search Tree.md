### Description

Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

**Input:** root = [2,1,3]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

**Input:** root = [5,1,4,null,null,3,6]
**Output:** false
**Explanation:** The root node's value is 5 but its right child's value is 4.

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-231 <= Node.val <= 231 - 1`

### Algorithm ([[Trees#Binary Tree|Binary Tree]])

1. each node needs to be between the min and max
2. if we are traversing left, set the max to node.val since the left node needs to be smaller
3. if we are traversing right, set the min to node.val since the right node needs to be larger
4. start min and max and negative and positive infinity

Gotchas
* don't just look at current node and compare that to left and right children. We need to track the max and min for the entire sub tree

### Solution

```
# time - O(n) where n is the number of nodes  
# space - O(n) n the number of nodes which is the worst case stack size  
class Solution:  
    def isValidBST(self, root: Optional[TreeNode]) -> bool:  
  
        def is_valid(node, minn, maxx):  
  
            if not node:  
                return True  
  
            if not minn < node.val < maxx:  
                return False  
  
            if not is_valid(node.left, minn, node.val) or not is_valid(node.right, node.val, maxx):  
                return False  
  
            return True  
        return is_valid(root, float("-inf"), float("inf"))
```

