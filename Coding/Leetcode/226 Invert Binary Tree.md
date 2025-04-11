### Description

Given the `root` of a binary tree, invert the tree, and return _its root_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

**Input:** root = [4,2,7,1,3,6,9]
**Output:** [4,7,2,9,6,3,1]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

**Input:** root = [2,1,3]
**Output:** [2,3,1]

**Example 3:**

**Input:** root = []
**Output:** []

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

### Algorithm ([[Trees#Binary Tree|Binary Tree]])

1. for each node, print the value
2. add the right node to the traversing queue
3. add the left node to the traversing queue
4. update the `node.left = node.right`
5. update the `node.right = node.left`

### Solution

```
# runtime - O(n) - we traverse each node
# space - O(w) - w is the width of the tree (aka max size of the traversing queue)
class Solution:  
  
    #         4  
    #       /   \    
    #      2     7    
    #     / \   / \    
    #    1   3 6   9  
    # Output    # [4,2,7,1,3,6,9]    # Expected    # [4,7,2,9,6,3,1]    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:  
        if not root:  
            return None  
  
        traversing_queue = [ root ]  
  
        while traversing_queue:  
            node = traversing_queue.pop(0)  
            if node.right:  
                # push the right node into queue first so it gets processed                      # first  
                traversing_queue.append(node.right)  
            if node.left:  
                traversing_queue.append(node.left)  
            # swap left and right values  
            left = node.left  
            right = node.right  
            node.left = right  
            node.right = left  
  
        return root
```