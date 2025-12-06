# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)

You are given an integer array <code>height</code> of length <code>n</code>. There are <code>n</code> vertical lines drawn such that the two endpoints of the <code>i^th</code> line are <code>(i, 0)</code> and <code>(i, height[i])</code>.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

**Notice**  that you may not slant the container.

**Example 1:** 
<img alt="" src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg" style="width: 600px; height: 287px;">

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

**Example 2:** 

```
Input: height = [1,1]
Output: 1
```

**Constraints:** 

- <code>n == height.length</code>
- <code>2 <= n <= 10^5</code>
- <code>0 <= height[i] <= 10^4</code>

---

# Solution

```python3
class Solution:
    def maxArea(self, height: List[int]) -> int:

        # Two pointers: one at the left end, one at the right end
        left = 0
        right = len(height) - 1

        # Variable to store the maximum area found so far
        area = 0

        # Continue until the two pointers meet
        while left < right:

            # The height of the container = minimum of the two heights
            # Width of the container = distance between left and right
            larea = min(height[left], height[right]) * (right - left)

            # Update maximum area if the current area is larger
            area = max(larea, area)

            # Pointer movement logic:
            # The area is limited by the smaller height.
            # To potentially find a larger area, we must move the pointer
            # at the smaller height inward, hoping to find a taller line.

            if height[left] > height[right]:
                # Right line is shorter → move right pointer left
                right -= 1
            else:
                # Left line is shorter or equal → move left pointer right
                left += 1

        # After exploring all possible pairs, return the maximum area found
        return area
```
