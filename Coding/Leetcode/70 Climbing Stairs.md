### Description

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2
**Output:** 2
**Explanation:** There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

**Example 2:**

**Input:** n = 3
**Output:** 3
**Explanation:** There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

**Constraints:**

- `1 <= n <= 45`

### Algorithm ([[Fibonacci]])

1. Since fib needs prev two totals calculated, return n if n <= 2
2. Init an array of size n + 1 where each index will store a fib value
	1. + 1 because we will be setting index 0 to 0
3. iterate from 3rd position to n + 1 (since we are already returning a solution if n <= 2)
	1. + 1 since second int in range is exclusive
	2. calculate fib by adding prev plus prev_prev
4. return totals[n]

### Solution

```
# runtime - O(n) where n is the number of stairs
# space - O(n) where n is the number of stairs. This is due to the array of totals
class Solution:  
  
    def climbStairs(self, n: int) -> int:  
        if n <= 2:  
            # 1 only has 1 way to climb  
            # 2 has 2 ways to climb            return n  
  
        # sets an array with all indexes to 0  
        totals = [0] * (n + 1)  
        totals[1] = 1  
        totals[2] = 2  
  
        # start at 3 since we already have returns for the first 2  
        for i in range(3, n + 1):  
            prev = i - 1  
            prev_prev = i - 2  
            totals[i] = totals[prev] + totals[prev_prev]  
  
        return totals[n]
```
