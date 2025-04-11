##### appending an array does not return a new instance of that array
* `graph[node1] = graph.get(node1).append(node2)`
	* this sets the array to None
	* instead do `graph.get(node1).append(node2)` 
