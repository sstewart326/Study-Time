### Description

Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]
**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]
**Output:** [0,0,9,0,0]

**Constraints:**

- `2 <= nums.length <= 105`
- `-30 <= nums[i] <= 30`
- The input is generated such that `answer[i]` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1)` extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

### Algorithm

1. Calculate the prefix products (left to right)
2. Calculate the postfix products (right to left)
3. for each index, multiply the prefix_prod - i * post_fix_prod + 1
	1. if either is out of bounds, multiply by 1

### Solution

```
# calculate prefixes and postfixes  
# [1, 2, 3, 4]     result ->     [24, 12, 8, 6]  
#  
# product -> (prefix)  
# [1, 2, 6, 24]  
# product <- (postfix)  
# [24, 24, 12, 4]  
#  
# now calculate the result my taking product of prefix before i and suffix after i  
  
# time - O(n) - iterate right to left to calculate the prefixes and left to right to calculate the suffixes  
# space - O(n) - output array  
class Solution:  
    def productExceptSelf(self, nums: List[int]) -> List[int]:  
  
        size = len(nums)  
        output = [1] * size  
  
        if size <= 1:  
            return nums  
  
        # calculate prefix  
        for i in range(size):  
            prev = 1 if i == 0 else output[i - 1]  
            output[i] = nums[i] * prev  
  
        # calculate postfix (products from last element to first)  
        # and then get the result (prev * next which excludes the curr element)  
        for j in range(size-1, -1, -1):  
  
            # calculating the suffix  
            prev_suffix = 1 if j+1 == size else nums[j+1]  
            nums[j] = nums[j] * prev_suffix  
  
            # determining the output by multiplying prev suffix and next prefix  
            next_prefix = 1 if j-1 < 0 else output[j-1]  
            prev_suffix = 1 if j+1 == size else nums[j+1]  
            output[j] = next_prefix * prev_suffix  
  
        return output
```

