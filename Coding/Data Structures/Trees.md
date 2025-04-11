#### Terminology

**node** - a point that holds some value
**root** - top most node with no parent
**edge** - connects a parent to a child
**leaf** - a node without a child

#### Binary Tree

```
    8         
   / \           Left child < parent node
  4   10         Right child > parent node
 / \    \        
2   5    12      Inorder Prints: 2, 4, 5, 8, 10, 12
```

 ##### Leetcode problems
* [[226 Invert Binary Tree]]
* [[235 Lowest Common Ancestor in Binary Tree]]
* [[110 Balanced Binary Tree]]
* [[543 Diameter of a Binary Tree]]
* [[104 Max Depth Binary Tree]]
* [[102 Binary Tree Level Order Traversal]]
#### Depth First Traversal

*Uses stacks*

```
    A         Preorder Prints: A, B, D, E, C, F
   / \          Prints on every node first visited
  B   C       Inorder Prints: D, B, E, A, F, C
 / \   \        Recursively prints every left node, then right
D   E   F     Postorder Prints: D, E, B, A, F, C
                Prints one layer at a time starting at bottom and working up 
```

###### Traversing Algorithm (applies to all types below)

`def traverse(node)`

1. return if node is null
2. traverse(node.left)
3. traverse(node.right)


###### Preorder Algorithm

```
FUNCTION preorderTraversal(node):
  IF node is null:
    RETURN
  
  # Visit the root node
  visit(node)
  
  # Recursively traverse the left subtree
  preorderTraversal(node.left)
  
  # Recursively traverse the right subtree
  preorderTraversal(node.right)
```

###### Inorder Algorithm

```
FUNCTION inorderTraversal(node):
  IF node is null:
    RETURN
  
  # Recursively traverse the left subtree
  inorderTraversal(node.left)
  
  # Visit the current node
  visit(node)
  
  # Recursively traverse the right subtree
  inorderTraversal(node.right)
```

###### Postorder Algorithm

```
FUNCTION postorderTraversal(node):
  IF node is null:
    RETURN
  
  # Recursively traverse the left subtree
  postorderTraversal(node.left)
  
  # Recursively traverse the right subtree
  postorderTraversal(node.right)
  
  # Visit the current node
  visit(node)
```

##### Leetcode problems

* [[543 Diameter of a Binary Tree]]
* [[104 Max Depth Binary Tree]]

#### Breadth First Traversal

*Uses Queues*

```
    A         Prints: A, B, C, D, E, F
   / \          
  B   C       
 / \   \        
D   E   F     
                
```

##### Leetcode Problems

* [[102 Binary Tree Level Order Traversal]]
###### Traversing Algorithm 

1. queue = [ root ]
2. while queue
3. do_something_with_val = queue.pop(0)
4. if root.left, queue.append
5. if root.right, queue.append