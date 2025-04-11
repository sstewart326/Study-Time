### Description

Given a binary tree, determine if it is **height-balanced**.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)

**Input:** root = [1,2,2,3,3,null,null,4,4]
**Output:** false

**Example 3:**

**Input:** root = []
**Output:** true

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `-104 <= Node.val <= 104`

### Algorithm [[Trees#Depth First Traversal|Tree DFT]]
1. Traverse depth first until we reach a leaf
2. Mark the height as 1
3. for each recursive call:
	1. Check if the `abs(left_height - right_height > 1` and return -1 if so
		1. -1 signifies that the tree is unbalanced
	2. for each node, if the left or right child returns -1, return -1 as well to propagate that
	3. else, take the max of the left and right height and add one to get the current node's height 

### Solution

```
#  
#        (4) 1  
#           / \  
#      (3) 2   2 (1)    left side height (4) is more than 1 time higher than the right side height (1)  
#         / \  
#    (2) 3   3  
#       /  
#  (1) 4  
# Traverse depth first  
# find the height of both the left and the right  
# the height represented at the parent node should reflect the max height of the subtree  
# for each node, check if the absolute value of the difference of the two is > 1 return -1  
# time - O(n) where n is each node. We need to visit each node exactly once  
# space - O(h) where h is the height of the tree. The solution is recursive which stacks calls as high as the tree  
class Solution:  
  
    def get_height(self, node: TreeNode) -> int:  
  
        # once we reach a None  
        if not node:  
            return 0  
  
        left_height = self.get_height(node.left)  
        right_height = self.get_height(node.right)  
  
        # If either subtree is unbalanced, propagate the failure (-1)  
        if left_height == -1 or right_height == -1:  
            return -1  
  
        # base case  
        if (abs(left_height-right_height)) > 1:  
            return -1  
  
        return max(left_height + 1, right_height + 1)  
  
    def isBalanced(self, root: Optional[TreeNode]) -> bool:  
        if root:  
            if self.get_height(root) == -1:  
                return False  
            else:  
                return True  
        else:  
            return True
```