### Description

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

Implement the `MyQueue` class:

- `void push(int x)` Pushes element x to the back of the queue.
- `int pop()` Removes the element from the front of the queue and returns it.
- `int peek()` Returns the element at the front of the queue.
- `boolean empty()` Returns `true` if the queue is empty, `false` otherwise.

**Notes:**

- You must use **only** standard operations of a stack, which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
- Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

**Example 1:**

**Input**
["MyQueue", "push", "push", "peek", "pop", "empty"]
\[[], [1], [2], [], [], []\]
**Output**
[null, null, null, 1, 1, false]

**Explanation**
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false

**Constraints:**

- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `peek`, and `empty`.
- All the calls to `pop` and `peek` are valid.

**Follow-up:** Can you implement the queue such that each operation is **[amortized](https://en.wikipedia.org/wiki/Amortized_analysis)** `O(1)` time complexity? In other words, performing `n` operations will take overall `O(n)` time even if one of those operations may take longer.
### Algorithm ([[Study Time/Coding/Data Structures/Stacks|Stacks]] and [[Queues]])

* Since a Stack FIFO and a Queue is LIFO, we need to work with two stacks to reverse the ordering
* create a push_stack and a pop_stack
* push_stack is used any time we push to the queue
* pop_stack is used any time we peek or pop
* all elements should either be in the push or pop stack
* so if we pop() and all elements are in the push_stack, we need to transfer the elements to the pop_stack() before we pop()

### Solution

```
# since we need to reverse the stack, any time we need to pop or peek,  
# we should transfer all values from the push_stack to the peek_stack  
class MyQueue:  
  
    def __init__(self):  
        self.push_stack = []  
        self.pop_stack = []  
  
  
    def push(self, x: int) -> None:  
        if len(self.pop_stack) > 0:  
            self.transfer()  
        return self.push_stack.append(x)  
  
  
    def pop(self) -> int:  
        if len(self.push_stack) > 0:  
            self.transfer()  
        if len(self.pop_stack) > 0:  
            return self.pop_stack.pop()  
        else:  
            return -1  
  
    def peek(self) -> int:  
        if len(self.push_stack) > 0:  
            self.transfer()  
        if len(self.pop_stack) > 0:  
            return self.pop_stack[-1]  
        else:  
            return -1  
  
    def empty(self) -> bool:  
        return len(self.push_stack) == 0 and len(self.pop_stack) == 0  
  
    def transfer(self):  
        push_length = len(self.push_stack)  
        pop_length = len(self.pop_stack)  
        if push_length > 0:  
            while len(self.push_stack) > 0:  
                self.pop_stack.append(self.push_stack.pop())  
        if pop_length > 0:  
            while len(self.pop_stack) > 0:  
                self.push_stack.append(self.pop_stack.pop())
```
