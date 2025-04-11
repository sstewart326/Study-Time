### Description

Given two strings `ransomNote` and `magazine`, return `true` _if_ `ransomNote` _can be constructed by using the letters from_ `magazine` _and_ `false` _otherwise_.

Each letter in `magazine` can only be used once in `ransomNote`.

**Example 1:**

**Input:** ransomNote = "a", magazine = "b"
**Output:** false

**Example 2:**

**Input:** ransomNote = "aa", magazine = "ab"
**Output:** false

**Example 3:**

**Input:** ransomNote = "aa", magazine = "aab"
**Output:** true

**Constraints:**

- `1 <= ransomNote.length, magazine.length <= 105`
- `ransomNote` and `magazine` consist of lowercase English letters.

### Algorithm ([[Hash Map]])

* for each character in magazine, store it in a dictionary with the count
* for each character in ransomNote, check if it exists in the dictionary
* if it doesn't or the count == 0, return False
* at the end, return True

### Solution

```
class Solution:  
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:  
        # for each char in magazine, add to dictionary with count  
        # for each char in ransomNote, lookup from dictionary and subtract count        #     if char doesn't exist or count is 0 before we subtract, return false  
        chars = {}  
        for c in magazine:  
            if c in chars:  
                count = chars.get(c)  
                chars[c] = count + 1  
            else:  
                chars[c] = 1  
        for c in ransomNote:  
            if c not in chars:  
                return False  
            elif chars.get(c) == 0:  
                return False  
            else:  
                count = chars.get(c) - 1  
                chars[c] = count  
        return True
```

