### Description

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example 1:**

**Input:** n = 5, bad = 4
**Output:** 4
**Explanation:**
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.

**Example 2:**

**Input:** n = 1, bad = 1
**Output:** 1

**Constraints:**

- `1 <= bad <= n <= 231 - 1`

### Algorithm ([[Binary Search]])

* `low = 1, high = n`
* `index_to_check = low + (high - low) // 2`
	* we do `high - low` above to prevent int overflow if we are adding two large ints
* if the `index_to_check` is bad, we need to traverse the left so we set the high to `index_to_check` and recurse
* if `index_to_check` is good, we need to check to the right. Since we know `index_to_check` is good, we can increment it by one and set it to `low` to narrow the search
* return `low` when `low` is bad or `low` == `high`
	* since we are given the constraint that at least one version is bad

### Solution

```
class Solution:  
  
    # for each iteration, check (high + low) / 2  
    # once low >= high, return -1    # 1 2 3 4 5     4 is first bad index    # ^       ^    1 + (5 - 1) / 2 = 3    # 1 2 3 4 5    3 is not bad, increment 3 by one and set this to low    #     ^   ^    # 1 2 3 4 5    #       ^ ^    4 is bad. it is also low so we know there is no bad lower and we can return    def traverse(self, low, high):  
        # we can prevent stacked calls by returning early here  
        # this is the lowest value we've seen so far so if it is bad, we can return        if isBadVersion(low):  
            return low  
  
        # given we know there is at least one bad version, once low >= high, we can return low  
        if low >= high:  
            return low  
  
        # prevents int overflows. better this than high + low // 2  
        index_to_check = low + (high - low) // 2  
        if isBadVersion(index_to_check):  
            # continue to search left half  
            return self.traverse(low, index_to_check)  
        else:  
            #,continue to search right half but start at index_to_check + 1  
            # since we know index_to_check is not bad            return self.traverse(index_to_check + 1, high)  
  
    def firstBadVersion(self, n: int) -> int:  
        return self.traverse(1, n)
```

