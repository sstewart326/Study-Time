### Description ([[Study Time/Coding/Algorithms/Stacks| Stack Problems]])

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"

**Output:** true

**Example 2:**

**Input:** s = "()[]{}"

**Output:** true

**Example 3:**

**Input:** s = "(]"

**Output:** false

**Example 4:**

**Input:** s = "([])"

**Output:** true

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.

### Algorithm
* push each starting parenthesis character into a stack
* when we reach an ending character, check if the stack has elements
	* if so, pop the stack
		* the popped char needs to be the starting parenthesis
			* if it is not, return `False` 
	* else return `False`
		* an ending character needs to be preceded by a starting character
* after everything has been iterated, check that the stack is empty
	* if so, all our starting characters had endings and we return `True`
	

### Solution

```
# runtime is O(n) - we need to visit each character in the string once  
# runtime is O(n) - we are pushing characters into a stack  
def is_valid(s):  
    # push onto stack if not a closing bracket  
    # pop from stack if closing bracket        # if popped value is not opening char, return false    # return true at end  
    stack = []  
    for c in s:  
        if c != ')' and c != '}' and c != ']':  
            stack.append(c)  
        elif len(stack) > 0:  
            popped = stack.pop()  
            if c == ')' and popped != '(':  
                return False  
            elif c == ']' and popped != '[':  
                return False  
            if c == '}' and popped != '{':  
                return False  
        else:  
            return False  
    return len(stack) == 0
```