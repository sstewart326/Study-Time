### Description

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [-1,0,3,5,9,12], target = 9
**Output:** 4
**Explanation:** 9 exists in nums and its index is 4

**Example 2:**

**Input:** nums = [-1,0,3,5,9,12], target = 2
**Output:** -1
**Explanation:** 2 does not exist in nums so return -1

**Constraints:**

- `1 <= nums.length <= 104`
- `-104 < nums[i], target < 104`
- All the integers in `nums` are **unique**.
- `nums` is sorted in ascending order.

### Algorithm ([[Binary Search]])

1. keep track of `low_index` and `high_index`
2. while the `low_index <= high_index` 
	1. calculate a `target_index` via `(high - low) // 2`
	2. if `target_index` hold the target, return that index
	3. else if the value is greater than our target, the target lies to the left so set the `high_index = target_index - 1`
	4. else if the value is less than our target, the target lies to the right so set the `low_index = target_index + 1`

### Solution

```
# runtime - O(logn) - each iteration cuts the list in half  
# space - O(1) - just keeping track of indexes  
class Solution:  
    def search(self, nums: List[int], target: int) -> int:  
  
        # keep track of low index and high index  
        # [-1,0,3,5,9,12]  target 9        
        #   l   ^      h   int((5 + 0) / 2) = 2        
        #                  3 < 9 so set low index to 2        
        #                  int((5 + 2) / 2) = 3        
        # [-1,0,3,5,9,12]  target 9        
        #       l ^   h    5 < 9 so set low index to 3        
        #                  int((5+3) / 2) = 4)        
        # [-1,0,3,5,9,12]  target 9        
        #         l ^ h    9 == 9, return index  
        low_idx = 0  
        high_idx = len(nums) - 1  
  
        while low_idx <= high_idx:  
            target_idx = int((high_idx + low_idx) / 2)  
            if nums[target_idx] == target:  
                return target_idx  
            elif nums[target_idx] > target:  
                high_idx = target_idx - 1  
            else:  
                low_idx = target_idx + 1  
  
        return -1

```