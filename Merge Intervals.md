# [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/description/)

Given an arrayof <code>intervals</code>where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

**Example 1:** 

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

**Example 2:** 

```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

**Example 3:** 

```
Input: intervals = [[4,7],[1,4]]
Output: [[1,7]]
Explanation: Intervals [1,4] and [4,7] are considered overlapping.
```

**Constraints:** 

- <code>1 <= intervals.length <= 10^4</code>
- <code>intervals[i].length == 2</code>
- <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10^4</code>


# Solution

```py
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:

        # This will store the final merged intervals
        res = []

        # Total number of intervals
        n = len(intervals)

        # Sort intervals by starting time.
        # Sorting is required so overlapping intervals become adjacent.
        intervals.sort()

        # 'l' will point to the start of a potential merge group
        l = 0

        # Loop until we process all intervals
        while l < n:

            # Take the first interval in the current group
            ll, lh = intervals[l]   # ll = left/start, lh = right/end

            # r pointer to check next intervals
            r = l + 1

            # Keep merging all intervals that overlap with [ll, lh]
            while r < n:
                rl, rh = intervals[r]

                # Overlap condition:
                # If next interval's start <= current interval's end,
                # they overlap and can be merged.
                if lh >= rl:
                    # Expand the current group end
                    lh = max(lh, rh)
                    r += 1
                else:
                    # No overlap → break and start a new group
                    break

            # Add the fully merged interval to result
            res.append([ll, lh])

            # Move 'l' to the next unprocessed interval
            l = r

        # Return all merged intervals
        return res

```
