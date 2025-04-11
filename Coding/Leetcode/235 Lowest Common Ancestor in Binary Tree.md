### Description

Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

**Input:** root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
**Output:** 6
**Explanation:** The LCA of nodes 2 and 8 is 6.

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

**Input:** root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
**Output:** 2
**Explanation:** The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

**Example 3:**

**Input:** root = [2,1], p = 2, q = 1
**Output:** 2

**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the BST.

### Algorithm ([[Trees#Binary Tree|Binary Tree]])

Since this is a binary tree, we can make assumptions on the ordering
1. if p is less than the node and q is greater than the node OR vice versa, we return the node because this is the lowest common ancestor
2. if the current node equals q or p, return the node
3. if both are less than root, we traverse the left recursively
4. if both are greater than root, we traverse right recursively

### Solution

```
#  
#        6  
#       /  \  
#      /    \        p=3      p=2          p=2           p=2  
#     2      8       q=9      q=8          q=4           q=1 (doesn't exit)  
#    / \    / \      lca=6    lca=6        lca=2         lca=2  
#   0   4   7  9  
#      / \  
#     3   5  
# because this is a binary tree we can assume the following  
#   if p or q is less than curr node and the other p or q is greater than curr node, we are at the lca  
#   else traverse left if both numbers are less than node  
#        traverse right if both numbers are greater than node  
#   if curr node equals p or q, return curr node  
# runtime - O(h) - h is the height of the tree. We visit a max h nodes  
# space - O(h) - h is the height of the tree. we are stacking calls since this is recursive  
class Solution:  
  
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':  
        if p.val < root.val and q.val > root.val:  
            return root  
        elif p.val > root.val and q.val < root.val:  
            return root  
        elif p.val == root.val or q.val == root.val:  
            return root  
        elif p.val < root.val:  
            return self.lowestCommonAncestor(root.left, p, q)  
        else:  
            return self.lowestCommonAncestor(root.right, p, q)
```