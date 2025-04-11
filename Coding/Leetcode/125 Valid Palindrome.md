### Description

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` _if it is a **palindrome**, or_ `false` _otherwise_.

**Example 1:**

**Input:** s = "A man, a plan, a canal: Panama"
**Output:** true
**Explanation:** "amanaplanacanalpanama" is a palindrome.

**Example 2:**

**Input:** s = "race a car"
**Output:** false
**Explanation:** "raceacar" is not a palindrome.

**Example 3:**

**Input:** s = " "
**Output:** true
**Explanation:** s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

**Constraints:**

- `1 <= s.length <= 2 * 105`
- `s` consists only of printable ASCII characters.

### Algorithm ([[Study Time/Coding/Algorithms/Two Pointer|Two Pointer]])

1. left pointer = 0
2. right pointer = `len(s)-1`
3. while the left pointer value is not alphanumeric and left pointer is less than right, increment left pointer
	1. because the string can have spaces or special characters
4. while the right pointer is not alphanumeric and left pointer is less than right, decrement right pointer
5. compare left and right character and return false if they do not match
6. return true at the end if left pointer >= right pointer
	1. signifies we've traversed each character

### Solution

```
# time complexity - O(N) - at best we only traverse the strings to the mid-point  
# space complexity - O(1) - re-using i, j  
class Solution:  
    def isPalindrome(self, s: str) -> bool:  
        # racecar  
        # ^     ^  
        if len(s) == 1:  
            return True  
  
        i = 0  
        j = len(s) - 1  
  
        while i < j:  
            while i < j and not s[i].isalnum():  
                i += 1  
            while i < j and not s[j].isalnum():  
                j -= 1  
            if s[i].lower() != s[j].lower():  
                return False  
            i+=1  
            j-=1  
        return True
```
