### Description

Given a string `s` which consists of lowercase or uppercase letters, return the length of the **longest palindrome** that can be built with those letters.

Letters are **case sensitive**, for example, `"Aa"` is not considered a palindrome.

**Example 1:**

**Input:** s = "abccccdd"
**Output:** 7
**Explanation:** One longest palindrome that can be built is "dccaccd", whose length is 7.

**Example 2:**

**Input:** s = "a"
**Output:** 1
**Explanation:** The longest palindrome that can be built is "a", whose length is 1.

**Constraints:**

- `1 <= s.length <= 2000`
- `s` consists of lowercase **and/or** uppercase English letters only.

### Algorithm ([[Sets]])

A palindrome is symmetric on both sides but can allow a unique character in the middle . So our algorithm needs to track even occurrences of characters but allow 1 odd character

1. initialize a character set and a return var `length`. The set is going to track odd and even occurrences of a character. If the set has a character, that character currently has an odd count
2. iterate over the `str`. If the current character is in the set, remove it and increment the length by 2
3. at the end, if we still have a character in the set, increment the length by 1 to allow one odd character

### Solution

```
class Solution:  
  
    # a palindrome is symmetric on both sides but can allow a unique character in the middle  
    # so our algorithm needs to track even occurrences of characters but allow 1 odd character  
    # runtime - o(c) where c is the number of characters    # space - o(c) worst case, our str has all unique characters and our set fills up    def longestPalindrome(self, s: str) -> int:  
        # to keep track of chars with odd frequencies  
        chars = set()  
        # our return var  
        length = 0  
  
        for c in s:  
            # if c count is even, add 2 to the length  
            if c in chars:  
                chars.discard(c)  
                length += 2  
            # else add the first occurence to the set  
            else:  
                chars.add(c)  
  
        # if there is a char with an odd length, add 1 to the length  
        if len(chars) > 0:  
            return length + 1  
        # else just return the length  
        else:  
            return length
            
```
