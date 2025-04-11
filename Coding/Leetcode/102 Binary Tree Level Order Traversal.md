### Description

Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** [[3],[9,20],[15,7]]

**Example 2:**

**Input:** root = [1]
**Output:** [[1]]

**Example 3:**

**Input:** root = []
**Output:** []

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-1000 <= Node.val <= 1000`

### Algorithm ([[Trees#Binary Tree|Binary Tree]] | [[Trees#Breadth First Traversal|BFT]]))

1. the usual BFT but each element in the queue is an array of the nodes at a particular level

### Solution

```
# time - O(n) where n is the nodes in the tree  
# space - O(n) due to the answer array holding n nodes  
class Solution:  
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:  
        if not root:  
            return []  
  
        queue = [ [root] ]  
        answer = []  
  
        while queue:  
            level = queue.pop(0)  
            level_values = list(map(lambda node: node.val, level))  
            answer.append(level_values)  
            curr_level = []  
            for node in level:  
                if node.left:  
                    curr_level.append(node.left)  
                if node.right:  
                    curr_level.append(node.right)  
            if curr_level:  
                queue.append(curr_level)  
  
        return answer
```