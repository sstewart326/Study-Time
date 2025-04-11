### Description

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** 3

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]
**Output:** 2

**Constraints:**

- `n == nums.length`
- `1 <= n <= 5 * 104`
- `-109 <= nums[i] <= 109`

**Follow-up:** Could you solve the problem in linear time and in `O(1)` space?

### Algorithm ([[Boyer-Moore Voting Algorithm]])

* initiate `curr_majority, count = None, 0`
* iterate over the nums
	* any time the count == 0, set curr_majority to the num and count to 1
	* else if the curr_majority == num, increment the count
	* else the curr_majority != num and we need to decrement the count

### Solution

```
# Input: nums = [2,2,1,1,1,2,2]  
# Output: 2  
#  
# var to track curr_majority, count  
#  
# iterate nums  
# if count = 0  
#     set current_majority to num and increment count  
# if curr_majority == curr  
#     increment count  
# if curr_majority != curr  
#     decrement count  
# time - O(n) where n is the number of nums  
# space - O(1) we are only tracking count and curr_majority  
class Solution:  
    def majorityElement(self, nums: List[int]) -> int:  
  
        curr_majority = None  
        count = 0  
  
        for num in nums:  
            if count == 0:  
                curr_majority = num  
                count += 1  
            elif curr_majority == num:  
                count += 1  
            else:  
                count -= 1  
  
        return curr_majority
```