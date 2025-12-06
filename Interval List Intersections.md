# [986. Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/description/)

You are given two lists of closed intervals, <code>firstList</code> and <code>secondList</code>, where <code>firstList[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> and <code>secondList[j] = [start<sub>j</sub>, end<sub>j</sub>]</code>. Each list of intervals is pairwise **disjoint**  and in **sorted order** .

Return the intersection of these two interval lists.

A **closed interval**  <code>[a, b]</code> (with <code>a <= b</code>) denotes the set of real numbers <code>x</code> with <code>a <= x <= b</code>.

The **intersection**  of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of <code>[1, 3]</code> and <code>[2, 4]</code> is <code>[2, 3]</code>.

**Example 1:** 
<img alt="" src="https://assets.leetcode.com/uploads/2019/01/30/interval1.png" style="width: 700px; height: 194px;">

```
Input: firstList = [[0,2],[5,10],[13,23],[24,25]], secondList = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```

**Example 2:** 

```
Input: firstList = [[1,3],[5,9]], secondList = []
Output: []
```

**Constraints:** 

- <code>0 <= firstList.length, secondList.length <= 1000</code>
- <code>firstList.length + secondList.length >= 1</code>
- <code>0 <= start<sub>i</sub> < end<sub>i</sub> <= 10^9</code>
- <code>end<sub>i</sub> < start<sub>i+1</sub></code>
- <code>0 <= start<sub>j</sub> < end<sub>j</sub> <= 10^9 </code>
- <code>end<sub>j</sub> < start<sub>j+1</sub></code>

# Solution

```py
class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        left, right = 0, 0
        res = list()
        while left < len(firstList) and right < len(secondList):
            start = max(firstList[left][0], secondList[right][0])
            end = min(firstList[left][1], secondList[right][1])
            if start <= end:
                res.append([start, end])
            if firstList[left][1] < secondList[right][1]:
                left += 1
            else:
                right += 1
        return res
```
