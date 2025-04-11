### Description

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

**Example 1:**

**Input:** s = "anagram", t = "nagaram"

**Output:** true

**Example 2:**

**Input:** s = "rat", t = "car"

**Output:** false

**Constraints:**

- `1 <= s.length, t.length <= 5 * 104`
- `s` and `t` consist of lowercase English letters.

**Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

**Answer:** 
- **Memory usage**: With Unicode, the potential character set is much larger (over 143,000 characters), so the hash tables could theoretically grow larger. In practice, most texts use a limited subset of Unicode.
- **Hash efficiency**: Python's dictionaries and Counter objects handle Unicode characters efficiently, so the performance impact should be minimal.
- **String processing**: Python 3 natively supports Unicode, so the code doesn't require modification.
### Algorithm ([[Hash Map]])

1. if the strings are not of equal length return false
2. iterate the first string and add each character to a dictionary with counts
3. iterate the second string and lookup the character in the dictionary
	1. if the c is not in the dictionary, return false
	2. if the count is 0, return False
	3. decrement the count otherwise

### Solution ()

```
# time complexity - O(n) - because worst case, we visit each character in both strings m + n  
# space complexity - O(k) - k is the ASCII characters  
class Solution:  
  
    def isAnagram(self, s: str, t: str) -> bool:  
        # Early length check  
        if len(s) != len(t):  
            return False  
  
        # Create frequency dictionary in one pass  
        char_count = {}  
        for c in s:  
            char_count[c] = char_count.get(c, 0) + 1  
  
        # Decrement counts in one pass  
        for c in t:  
            if c not in char_count or char_count[c] == 0:  
                return False  
            char_count[c] -= 1  
  
        return True
```