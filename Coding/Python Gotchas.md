###### appending an array does not return a new instance of that array
* `graph[node1] = graph.get(node1).append(node2)`
	* this sets the array to None
	* instead do `graph.get(node1).append(node2)` 
* "".isdigit or "".isnumeric will return false for negative numbers
* `if not some_var` doesn't just check if not None. It will also return false if 0

###### init an array of certain size
`inited_arr = [0] * len(nums)`