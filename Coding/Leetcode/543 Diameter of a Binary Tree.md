### Description

Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

**Input:** root = [1,2,3,4,5]
**Output:** 3
**Explanation:** 3 is the length of the path [4,2,1,3] or [5,2,1,3].

**Example 2:**

**Input:** root = [1,2]
**Output:** 1

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-100 <= Node.val <= 100`

### Algorithm ([[Trees#Depth First Traversal]])

Note - this one is tricky because we need to track not only height, but `max_diameter`. This is because we can not determine a max_diameter at the root node since a subtree can have a larger max_diamter. See the example trees below for an example.

`diameter = left_height + right_height`

1. base cases
	1. if the node is not defined, return 0 for the height and 0 for the max_diameter
	2. if the node is a leaf, return 1 for the height and 1 for the max_diameter
2. at each node, calculate the height by taking the max of the left and right height
3. at each node, calculate the diameter then return the max_diameter. The `max_diameter` is the max of the `left_max`, `right_max` and `(left_height + right_height)`

### Solution

```
#          1                                                       1  diam = 4, h = 3  
#         / \                                                       \  
# (3)    2   4  (1)        diameter = 4                              2  diam = 4, h = 2  
#       / \                                                         / \  
# (2)  5   3 (1)                                  diam = 1 h = 1   3   4 diam = 1 h = 1  
#     /                                                           /     \  
#(1) 6                                      diam = 0 height = 0  5       6 diam = 0 height = 0  
#  
#  
# need to track two things  
#   height: max(left, right)  
#   diameter: left + right + 1 (to account for our current node)  
# when we reach a leaf, return 1  
# diameter formula - left_height + right_height  
# height formula - max(left_height, right_height)  
  
# time - O(n) where n is each node  
# space - O(n) for a completely unbalanced tree. O(logn) for a balanced tree. This is due to #         the stack recursion  
class Solution:  
  
    Height = NewType('height', int)  
    Diameter = NewType('diameter', int)  
  
    def recurse(self, node) -> (Height, Diameter):  
        if not node:  
            return 0, 0  
        if not node.left and not node.right:  
            return 1, 1  
  
        left_height, left_diameter = self.recurse(node.left)  
        right_height, right_diameter = self.recurse(node.right)  
  
        # diameter is taking max of heights and diameters because already calculated diameters could  
        # be taller than the current left_height + right_height        return max(left_height, right_height) + 1, max(left_height + right_height, right_diameter, left_diameter)  
  
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:  
        if not root or (not root.left and not root.right):  
            return 0  
        return self.recurse(root)[1]
```