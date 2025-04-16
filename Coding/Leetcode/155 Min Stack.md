### Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Example 1:**

**Input**
["MinStack","push","push","push","getMin","pop","top","getMin"]
\[[],[-2],[0],[-3],[],[],[],[]\]

**Output**
[null,null,null,null,-3,null,0,-2]

**Explanation**
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2

**Constraints:**

- `-231 <= val <= 231 - 1`
- Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
- At most `3 * 104` calls will be made to `push`, `pop`, `top`, and `getMin`.

### Algorithm ([[Stacks]])

1. for each push, track the min by looking at the previous element's min in the stack

### Solution

```
class MinStack:  
  
    def __init__(self):  
        # (val, lowest)  
        self.stack: [(int, int)] = []  
  
    def push(self, val: int) -> None:  
        curr_min = self.getMin()  
        this_min = val if curr_min is None or val < curr_min else curr_min  
        self.stack.append((val, this_min))  
  
    def pop(self) -> None:  
        self.stack.pop()  
  
    def top(self) -> int:  
        if len(self.stack) > 0:  
            return self.stack[-1][0]  
  
    def getMin(self) -> int:  
        if len(self.stack) > 0:  
            return self.stack[-1][1]
```

