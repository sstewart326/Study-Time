### Description

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance (i.e., `√(x1 - x2)2 + (y1 - y2)2`).

You may return the answer in **any order**. The answer is **guaranteed** to be **unique** (except for the order that it is in).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/closestplane1.jpg)

**Input:** points = \[[1,3],[-2,2]\], k = 1
**Output:** \[[-2,2]\]
**Explanation:**
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just \[[-2,2]\].

**Example 2:**

**Input:** points = \[[3,3],[5,-1],[-2,4]\], k = 2
**Output:** \[[3,3],[-2,4]\]
**Explanation:** The answer \[[-2,4],[3,3]\] would also be accepted.

**Constraints:**

- `1 <= k <= points.length <= 104`
- `-104 <= xi, yi <= 104`

### Algorithm ([[Heaps#Min Heap]])

1. calculate distance for each point
2. `if len(heap) < k` add the point to the heap (`heappush`)
	1. since `heapq` uses a min heap (pop removes the smallest item), negate each point before pushing so that when we pop, we pop the longest distance items
3. else pushpop (`heappushpop`) to push an element and the pop the k + 1 largest
### Solution

```
class Solution:  
  
    # The distance between two points on the X-Y plane is the Euclidean distance  
    # (i.e., √(x1 - x2)2 + (y1 - y2)2).    # x2 and y2 are the origin (0, 0) so we can remove those from the formula    # square root isn't really relevant because we don't need to return the exact distance    # rather we are just trying to identify which is closer. So we can remove that as well.    # so our formula becomes x**2 + y**2    def distance_between(self, x, y) -> int:  
        return x**2 + y**2  
  
  
    # time - O(n log k) we iterate through all points and log k for the operations on the heap (heappush, heappushpop)  
    # space - O(k) heap that stores at most k items    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:  
        heap = []  
  
        for point in points:  
            x, y = point[0], point[1]  
            if len(heap) < 2:  
                # negate the value because heapq uses min heap (pops lowest)  
                # we want the lowest number to become the highest number                heapq.heappush(heap, (-self.distance_between(x, y), x, y))  
            else:  
                # pops smallest number  
                heapq.heappushpop(heap, (-self.distance_between(x, y), x, y))  
  
        return [(x, y) for _, x, y in heap]
```