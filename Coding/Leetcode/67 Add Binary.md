### Description

Given two binary strings `a` and `b`, return _their sum as a binary string_.

**Example 1:**

**Input:** a = "11", b = "1"
**Output:** "100"

**Example 2:**

**Input:** a = "1010", b = "1011"
**Output:** "10101"

**Constraints:**

- `1 <= a.length, b.length <= 104`
- `a` and `b` consist only of `'0'` or `'1'` characters.
- Each string does not contain leading zeros except for the zero itself.

### Algorithm

1. track a remainder, solution array, and pointer
2. set the pointer to the end of both strings
3. while one string still has digits to iterate
	1. if one string does not have digits on the current index, set its value to 0
	2. else get the strings' values and add them together plus the remainder
		1. if the sum is < 2, there is no remainder to deal with and we can prepend the solution array with our sum. Set the remainder to 0
		2. otherwise, we can take the sum % 2 and prepend that to the solution array and set the remainder to 1
4. at the end, if there is still a remainder, prepend it to the solution array

### Solution

```
# Input: a = "1010", b = "1011"  
# Output: "10101"  
#  
#   need to track: right_pos, remainder  
#   to calculate curr (top + bottom + remainder)  
#       if that is 2, set curr to 0 and set remainder = 1  
#       elseif 3, set curr to 1 and set remainder = 0  
#       else set curr to sum and remainder = 0  
#  
#     1 0 1 0  
#           ^  
#     1 0 1 1  
#           ^  
# remainder = 0, sol = []  
#  1 + 0 == 1, sol = [1], remainder = 0  
#  
#     1 0 1 0  
#         ^  
#     1 0 1 1  
#         ^  
# 1 + 1 + 0 == 2, sol = [0, 1], remainder = 1  
#  
#     1 0 1 0  
#       ^  
#     1 0 1 1  
#       ^  
# 0 + 0 + 1 == 1, sol = [1, 0, 1], remainder = 0  
#  
#     1 0 1 0  
#     ^  
#     1 0 1 1  
#     ^  
# 1 + 1 + 0 == 2, sol = [0, 1, 0, 1], remainder = 1  
#  
# if remainder > 0, add to sol  
#  [1, 0, 1, 0, 1]  
# time - O(n) where n is the largest of the two strings  
# space - O(n+1) where n is the largest of the two strings. Worst case, we add a remainder at the front (thus +1)  
class Solution:  
    def addBinary(self, a: str, b: str) -> str:  
        right_pos = 0  
        remainder = 0  
        solution = ""  
  
        while right_pos < len(a) or right_pos < len(b):  
            a_val = 0  
            b_val = 0  
  
            # get the top and bottom values  
            # if the right_pos has overlapped our final value, set the value to 0            if len(a) > right_pos:  
                index = len(a)-1-right_pos  
                a_val = int(a[index])  
            if len(b) > right_pos:  
                index = len(b)-1-right_pos  
                b_val = int(b[index])  
  
            sum = a_val + b_val + remainder  
  
            # no special handling if we are not dealing with a remainder  
            if sum < 2:  
                solution = str(sum) + solution  
                remainder = 0  
            # else the sum is either 2 or 3. Thus, we can take the modulus 2 calculate the curr position  
            else:  
                solution = str(sum % 2) + solution  
                remainder = 1  
  
            right_pos += 1  
  
        # if a remainder remains at the end, we need to prepend the solution with it  
        if remainder == 1:  
            return '1' + solution  
        else:  
            return solution
```

