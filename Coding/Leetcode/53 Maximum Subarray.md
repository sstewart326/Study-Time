### Description

Given an integer array `nums`, find the subarray with the largest sum, and return _its sum_.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**Output:** 6
**Explanation:** The subarray [4,-1,2,1] has the largest sum 6.

**Example 2:**

**Input:** nums = [1]
**Output:** 1
**Explanation:** The subarray [1] has the largest sum 1.

**Example 3:**

**Input:** nums = [5,4,-1,7,8]
**Output:** 23
**Explanation:** The subarray [5,4,-1,7,8] has the largest sum 23.

**Constraints:**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

### Algorithm ([[Kadane's Algorithm]])

* init `max_num` and `last_sum` to `nums[0]`
* for each num
	* set `last_sum` to either the `nums[i] + last_sum` or `nums[i]` 
		* since we don't care for the sum if it is actually less than the current value
	* set `max_num` if `last_sum` is greater

### Solution

```
# Input: nums = [-2,1,-3,4,-1,2,1,-5,4]  
# Output: 6  
# Explanation: The subarray [4,-1,2,1] has the largest sum 6.  
#  
#     3  -4   7 -5   3 -1 -6  9  
#  [-2, 1, -3, 4, -1, 2, 1, -5, 4]  
class Solution:  
  
    def maxSubArray(self, nums: List[int]) -> int:  
        if not nums:  
            return 0  
  
        max_num = nums[0]  
        last_sum = nums[0]  
          
        # [ 1, 2, 3, -1, 6]  
        6  
  
        for i in range(1, len(nums)):  
  
            # this is where we sum  
            # if the current value is greater than the sum, just take the current value            last_sum = max(nums[i], last_sum + nums[i])  
  
            # if curr is > max, set max  
            max_num = max(max_num, last_sum)  
  
        return max_num
```

