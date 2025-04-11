
### Description

Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** 3

**Example 2:**

**Input:** root = [1,null,2]
**Output:** 2

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `-100 <= Node.val <= 100`


### Algorithm ([[Trees#Depth First Traversal]])

just a DFT

### Solution

```
# time - O(n) where n is the number of nodes in the tree  
# space - O(h) where h is the height of the tree  
class Solution:  
  
    def dfs_recurse(self, root: Optional[TreeNode]):  
        if not root:  
            return 0  
        if not root.left and not root.right:  
            return 1  
  
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))  
  
  
    def dfs(self, root: Optional[TreeNode]) -> int:  
        if not root:  
            return 0  
  
        entry = root, 1  
        stack = [entry]  
        max_depth = 0  
  
        while stack:  
            node, depth = stack.pop()  
            max_depth = max(max_depth, depth)  
  
            # right pushed first, so left will be popped (processed) first  
            if node.right:  
                stack.append((node.right, depth + 1))  
            if node.left:  
                stack.append((node.left, depth + 1))  
  
        return max_depth  
  
    def maxDepth(self, root: Optional[TreeNode]) -> int:  
        # return self.dfs_recurse(root)  
        return self.dfs(root)
```
