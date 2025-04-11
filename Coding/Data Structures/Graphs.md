#### Terminology

**Node** - holds some data
**Edge** - connection between nodes
**Directed Graph** - can only travel in the direction that the edge allows
**Undirected Graph** - can travel in any direction
**Neighbor Node** - any node that is directly accessible from the current node
**Acyclic** - we can not end up at a same node twice
**Cyclic** - we can end up at a same node twice

#### Data Structure

[[Hash Map]]

```
{ node  neighbors
	a:   [b, c]                    a->b->d<-f
	b:   [d]                       ↓  ↑
	c:   [e]                       c->e    
	d:   []                        
	e:   [b]                       
	f:   [d]
}
```

#### Algorithms

###### Depth First Traversal

* keep traversing in the same direction until we reach an end, at which point we. pivot to another direction and keep traversing until that ends. Repeat until the end
* uses a stack

###### Breadth First Traversal

* keep traversing in a circle-like pattern where we visit all surrounding nodes
* this explores all the directions evenly
* uses a queue
* when to use
	* finding the shortest path
		* because it starts at some point and works its way out evenly

**Notes**
if we have disconnected components
* we need to iterate over all components and ignore any node already visited
	* within each iteration, we need to recurse neighbors and keep track of visited

#### Space Time Complexity

n = number of nodes
e = number of edges

**Time** - O(e)
**Space** - O(n)

Edges = $n^{2}$ 
Because at worst case, each node can have two edges
Therefore, Time also can be represented by O($n^{2}$)

#### Leetcode Problems
* [[733 Flood Fill]]





