### Description

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` _after the insertion_.

**Note** that you don't need to modify `intervals` in-place. You can make a new array and return it.

**Example 1:**

**Input:** intervals = \[[1,3],[6,9]\], newInterval = [2,5]
**Output:** \[[1,5],[6,9]\]

**Example 2:**

**Input:** intervals = \[[1,2],[3,5],[6,7],[8,10],[12,16]\], newInterval = [4,8]
**Output:** \[[1,2],[3,10],[12,16]\]
**Explanation:** Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

**Constraints:**

- `0 <= intervals.length <= 104`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 105`
- `intervals` is sorted by `starti` in **ascending** order.
- `newInterval.length == 2`
- `0 <= start <= end <= 105`

### Algorithm ([[Interval Merging]])

1. init a `return_list`
2. iterate intervals
3. if the `newInterval` < curr iteration, we can append the `return_list` and return that list + the tail of the intervals
4. else if the curr iteration > `newInterval`, we can append the `return_list`
5. else the `newInterval` is overlapping the current iteration
	1. we can now set a newInterval of the overlaps where we take the min of the lows and the maxes of the highs
6. then at the end of the loop, let's return the `return_intervals` with the `newInterval` appended

### Solution

```
# Example 1:  
# Input: intervals = [[1,3],[6,9]], newInterval = [2,5]  
# Output: [[1,5],[6,9]]  
#  
# Example 2:  
# Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]  
# Output: [[1,2],[3,10],[12,16]]  
# Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].  
#  
# time - O(n) - traversing through the intervals. each interval is only of size 2 so we are not nesting loop thus not n*m  
# space - O(n) - persisting those intervals into a new list  
class Solution:  
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:  
        # if newInterval < interval[i], append newInterval + interval[i:]  
        # if interval[i] < newInterval, append interval[i]        # else we are overlapping so take mins and maxes        # at the end, append newInterval to the result  
        return_intervals = []  
  
        for i in range(len(intervals)):  
            # the new interval fits in before the tail, so we can return  
            if newInterval[1] < intervals[i][0]:  
                return_intervals.append(newInterval)  
                return return_intervals + intervals[i:]  
            # the new interval fits before the current index  
            elif intervals[i][1] < newInterval[0]:  
                return_intervals.append(intervals[i])  
            # the new interval overlaps the current index  
            else:  
                newInterval = [min(intervals[i][0], newInterval[0]), max(intervals[i][1], newInterval[1])]  
  
        return_intervals.append(newInterval)  
        return return_intervals
```