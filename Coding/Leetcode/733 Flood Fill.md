### Description

You are given an image represented by an `m x n` grid of integers `image`, where `image[i][j]` represents the pixel value of the image. You are also given three integers `sr`, `sc`, and `color`. Your task is to perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**:

1. Begin with the starting pixel and change its color to `color`.
2. Perform the same process for each pixel that is **directly adjacent** (pixels that share a side with the original pixel, either horizontally or vertically) and shares the **same color** as the starting pixel.
3. Keep **repeating** this process by checking neighboring pixels of the _updated_ pixels and modifying their color if it matches the original color of the starting pixel.
4. The process **stops** when there are **no more** adjacent pixels of the original color to update.

Return the **modified** image after performing the flood fill.

**Example 1:**

**Input:** image = \[[1,1,1],[1,1,0],[1,0,1]\], sr = 1, sc = 1, color = 2

**Output:** \[[2,2,2],[2,2,0],[2,0,1]\]

**Explanation:**

![](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

From the center of the image with position `(sr, sc) = (1, 1)` (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.

Note the bottom corner is **not** colored 2, because it is not horizontally or vertically connected to the starting pixel.

**Example 2:**

**Input:** image = \[[0,0,0],[0,0,0]\], sr = 0, sc = 0, color = 0

**Output:** \[[0,0,0],[0,0,0]\]

**Explanation:**

The starting pixel is already colored with 0, which is the same as the target color. Therefore, no changes are made to the image.

**Constraints:**

- `m == image.length`
- `n == image[i].length`
- `1 <= m, n <= 50`
- `0 <= image[i][j], color < 216`
- `0 <= sr < m`
- `0 <= sc < n`

### Algorithm [[Graphs#Depth First Traversal|Graph DFT]] or [[Graphs#Breadth First Traversal|Graph BFT]]

##### Recursive Depth First Search
1. start with return conditions
	1. node already visited, coordinates out of bounds, etc
2. add current node to visited
3. do some action on current node
4. recurse to left, right, bottom, and top positions
5. return the graph
##### BFS Queue
1. add the first coordinates to a queue
2. while queue
	1. start with the negative conditions and continue
		1. node already visited, coordinates our of bounds, etc
	2. add current node to visited
	3. do some action on current node
	4. add left, right, bottom, top positions to the queue
	5. return the graph


### Solution

```
class Solution:  
  
    def flip_colors_bfs(self, image, row, column, starting_color, new_color, visited):  
  
        queue = [ (row, column) ]  
  
        while queue:  
            row, column = queue.pop(0)  
  
            if (row, column) in visited:  
                continue  
            if row < 0 or row >= len(image):  
                continue  
            if column < 0 or column >= len(image[0]):  
                continue  
            if image[row][column] != starting_color:  
                visited.add((row, column))  
                continue  
  
            visited.add((row, column))  
            image[row][column] = new_color  
  
            queue.append((row + 1, column))  
            queue.append((row - 1, column))  
            queue.append((row, column + 1))  
            queue.append((row, column - 1))  
  
        return image  
  
    def flood_fill_stack(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:  
        starting_color = image[sr][sc]  
        if starting_color == color:  
            return image  
        return self.flip_colors_bfs(image, sr, sc, starting_color, color, set())  
  
  
  
    # depth first solution  
    # time - O(n) - n is the number of nodes in the image    
	# space - O(n) - n is the number of nodes in the image    
	#         worst case is we only have one row of colors that need to be changed    def flip_colors(self, image, row, column, starting_color, new_color, visited):  
  
        # if row, column has been visited, return  
        # if row, column is out of bounds, return        
        # add row, column to visited        
        # if image[row][column] != starting_color return  
        # add row, column to visited        
        # set image[row][column] = new_color        
        # return image  
        if (row, column) in visited:  
            return  
        if row < 0 or row >= len(image):  
            return  
        if column < 0 or column >= len(image[0]):  
            return  
        if image[row][column] != starting_color:  
            return  
  
        visited.add((row, column))  
        image[row][column] = new_color  
  
        self.flip_colors(image, row + 1, column, starting_color, new_color, visited)  
        self.flip_colors(image, row - 1, column, starting_color, new_color, visited)  
        self.flip_colors(image, row, column + 1, starting_color, new_color, visited)  
        self.flip_colors(image, row, column - 1, starting_color, new_color, visited)  
  
        return image  
  
    def floodFill(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:  
        starting_color = image[sr][sc]  
        if starting_color == color:  
            return image  
        return self.flip_colors(image, sr, sc, starting_color, color, set())
```