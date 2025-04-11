
### Description

Given a string `s`, find the length of the **longest** **substring** without duplicate characters.

**Example 1:**

**Input:** s = "abcabcbb"
**Output:** 3
**Explanation:** The answer is "abc", with the length of 3.

**Example 2:**

**Input:** s = "bbbbb"
**Output:** 1
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**

**Input:** s = "pwwkew"
**Output:** 3
**Explanation:** The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

**Constraints:**

- `0 <= s.length <= 5 * 104`
- `s` consists of English letters, digits, symbols and spaces.

### Algorithm ([[Sliding Window]])

1. set left and right pointers to start of string
2. create a set for each character we visit and a var for longest
3. iterate through string, adding the characters into the set
	1. calculate the current length by taking left - right and set `longest` if necessary
4. if we come across a character we've seen
	1. remove left character from the set until the left character equals the right character
5. 

### Solution

```
# time - O(s) or 2s where s is  the size of the str because the right pointer  
#        traverses the entire string and the left pointer could also do the same  
# space - O(min(s, n) where s is unique characters that get saved to curr and n is  
#         the length of the string  
class Solution:  
    def lengthOfLongestSubstring(self, s: str) -> int:  
        chars = set()  
        left = 0  
        longest = 0  
  
        for right in range(len(s)):  
            while s[right] in chars:  
                chars.remove(s[left])  
                left += 1  
  
            chars.add(s[right])  
  
            # plus 1 since we start at 0 index  
            longest = max(longest, right - left + 1)  
  
        return longest
```
