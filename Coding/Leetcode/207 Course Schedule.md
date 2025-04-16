### Description

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**

**Input:** numCourses = 2, prerequisites = \[[1,0]\]
**Output:** true
**Explanation:** There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.

**Example 2:**

**Input:** numCourses = 2, prerequisites = \[[1,0],[0,1]\]
**Output:** false
**Explanation:** There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Constraints:**

- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- All the pairs prerequisites[i] are **unique**.

### Algorithm ([[Graphs#Depth First Traversal|Graph DFS]] or [[Graphs#Breadth First Traversal|Graph BFS]])

1. create an adjacency list for our courses and prerequisites
2. iterate over the courses while tracking the curr_path and memo
	1. we use curr_path to detect cycles and add a node the the set when we visit and remove before we return True
	2. we use memo to keep track of courses that we've already determined. This gets set after all neighbors have been visited
Gotchas
1. for each recursive iteration, check if the course is in the pre_req_map.
	1. it is not when we have reached a node with no neighbors
2. use a memo to track the already determined courses. Visited is not enough as this is just used to detect cycles along the current path
	1. memo is a global data-structure
	2. visited/curr_path is scoped to each path

### Solution

```
# time - o(v + e) where v is the courses and e is the prerequisites  
# space - o(v + e)  
#         pre_req_map - O(edges) where e is the prerequisites  
#         curr_path - O(vertices) where v is each course  
#         memo - O(vertices) where v is each course  
#         recursive stack - O(vertices) the call stack can traverse each course in the worst case
class Solution:  
  
    def get_pre_req_map(self, prerequisites):  
        pre_req_map = {}  
        for node in prerequisites:  
            course = node[0]  
            pre_req = node[1]  
  
            if course in pre_req_map:  
                pre_reqs = pre_req_map.get(course)  
                pre_reqs.append(pre_req)  
                pre_req_map[course] = pre_reqs  
            else:  
                pre_req_map[course] = [pre_req]  
  
        return pre_req_map  
  
    def can_complete(self, pre_req_map, course, curr_path, memo):  
        # Check if we already determined this course  
        if course in memo:  
            return memo[course]  
  
        # This signifies we have reached a course with no prerequisites  
        if not pre_req_map.get(course):  
            return True  
  
        # If we're visiting a course that's in our current path, we have a cycle  
        if course in curr_path:  
            return False  
  
        curr_path.add(course)  
        pre_reqs = pre_req_map.get(course)  
  
        for neighbor in pre_reqs:  
            # Break recursion early if one prerequisite course cannot be completed  
            if not self.can_complete(pre_req_map, neighbor, curr_path, memo):  
                memo[course] = False  
                return False  
        # Remove from current path, but remember the result. We've explored all neighbors  
        curr_path.remove(course)  
        memo[course] = True  
        return True  
    # n = 5  
    # [[0,1], [0,2], [1,3], [1,4], [3,4]]    #    #            0    #           / \    #          1   2    #         / \    #        3 - 4    #    # pre_req_map = { 0: [1, 2], 1: [3, 4], 3: [4] }    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:  
        pre_req_map = self.get_pre_req_map(prerequisites)  
  
        # holds values for if we already determined this course  
        memo = {}  
        for course in range(numCourses):  
            curr_path = set()  
            # we need to loop like this in case some parts of the matrix are not connected  
            # e.g. unrelated courses            if not self.can_complete(pre_req_map, course, curr_path, memo):  
                return False  
  
        return True
```