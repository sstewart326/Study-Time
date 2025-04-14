### Description

You are given an array of strings `tokens` that represents an arithmetic expression in a [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Evaluate the expression. Return _an integer that represents the value of the expression_.

**Note** that:

- The valid operators are `'+'`, `'-'`, `'*'`, and `'/'`.
- Each operand may be an integer or another expression.
- The division between two integers always **truncates toward zero**.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a **32-bit** integer.

**Example 1:**

**Input:** tokens = ["2","1","+","3","*"]
**Output:** 9
**Explanation:** ((2 + 1) * 3) = 9

**Example 2:**

**Input:** tokens = ["4","13","5","/","+"]
**Output:** 6
**Explanation:** (4 + (13 / 5)) = 6

**Example 3:**

**Input:** tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
**Output:** 22
**Explanation:** ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22

**Constraints:**

- `1 <= tokens.length <= 104`
- `tokens[i]` is either an operator: `"+"`, `"-"`, `"*"`, or `"/"`, or an integer in the range `[-200, 200]`.

### Algorithm ([[Study Time/Coding/Data Structures/Stacks|Stacks]])

We start with the operators because it is hard to identify negative integers
1. for each each operator, pop the stack twice and perform the operation.
	1. The first pop is the second number
	2. The second pop is the first number
2. push the result back to the stack
3. for each number, push onto the stack

### Solution

```
# Input: tokens = ["2","1","+","3","*"]  
# Output: 9  
# Explanation: ((2 + 1) * 3) = 9  
#  
# time - O(c) where c is the number of characters in the string  
# space - O(c) worst case is O(n/2) where stack contains all nums followed by operators  
class Solution:  
    def evalRPN(self, tokens: List[str]) -> int:  
        stack = []  
  
        for token in tokens:  
            # better to start with characters since negative ints are difficult to identify  
            if token in ["+", "-", "*", "/"]:  
                second_num = int(stack.pop())  
                first_num = int(stack.pop())  
  
                if token == '+':  
                    stack.append(first_num + second_num)  
                elif token == '-':  
                    stack.append(first_num - second_num)  
                elif token == '*':  
                    stack.append(first_num * second_num)  
                elif token == '/':  
                    # Integer division toward zero  
                    stack.append(int(first_num / second_num))  
            else:  
                stack.append(token)  
  
        return stack.pop()
```