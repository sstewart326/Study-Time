
### Description

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]
**Output:** [[-1,-1,2],[-1,0,1]]
**Explanation:** 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

**Example 2:**

**Input:** nums = [0,1,1]
**Output:** []
**Explanation:** The only possible triplet does not sum up to 0.

**Example 3:**

**Input:** nums = [0,0,0]
**Output:** [[0,0,0]]
**Explanation:** The only possible triplet sums up to 0.

**Constraints:**

- `3 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`

### Algorithm ([[Study Time/Coding/Algorithms/Two Pointer|Two Pointer|Two Pointer]] | [[1 Two Sum]])

1. Order the list
2. Split this solution two parts
	1. iterate i over the nums
	2. for each iteration, solve the two sum by using `-num[i]` as the target
3. Two sum part:
	1. `left = i + 1` and `right = len(nums) - 1`
	2. if the left + right == target, store these in an array
		1. increment left and decrement right to move on to other possible solutions
	3. if left + right < target, increment left to increase the sum
	4. else if left + right > target, decrement right to decrease the sum

Gotchas:
1. don't reprocess
	1. for the outer for loop, make sure we don't reprocess where `nums[i] == nums[i-1]`
	2. for the two-pointer part, do the same and make sure we don't reprocess the `nums[left]`
		1. `if left > left_start and nums[left] == nums[left - 1]: left +=1`

### Solution

```
# time - O(n**2) - two pointer in nested. so outer loop runs through all numbers and the two pointer runs n-i number of times  
# space - O(n) for the answer list  
class Solution:  
  
    def find_target(self, nums: List[int], target, left, right) -> List[List[int]]:  
        answer = []  
        left_start = left  
        while left < right:  
            # if we've already found all sums for this number, continue  
            if left > left_start and nums[left] == nums[left - 1]:  
                left += 1  
                continue  
            if nums[left] + nums[right] == target:  
                answer.append([-target, nums[left], nums[right]])  
                left += 1  
                right -= 1  
                continue  
  
            # move left to increase sum  
            # move right to decrease sum            sum = nums[left] + nums[right]  
            if sum < target:  
                left += 1  
            else:  
                right -= 1  
  
        return answer  
  
  
    def threeSum(self, nums: List[int]) -> List[List[int]]:  
        answer: List[List[int]] = []  
        sorted_nums = sorted(nums)  
  
        # split this problem into 2  
        # use i to create a target sum        # then pass this target to another function to calculate 2sum        for i in range(len(nums) - 2):  
            l, r = i + 1, len(nums) - 1  
  
            # when we have already determined all possible sums for this target, continue  
            if i > 0 and sorted_nums[i] == sorted_nums[i-1]:  
                continue  
  
            # target sum is just the inverse of i  
            target = -sorted_nums[i]  
  
            answer = answer + self.find_target(sorted_nums, target, l, r)  
  
        return list(answer)
```
