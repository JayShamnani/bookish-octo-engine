# [15. 3Sum](https://leetcode.com/problems/3sum/description/)

Given an integer array nums, return all the triplets <code>[nums[i], nums[j], nums[k]]</code> such that <code>i != j</code>, <code>i != k</code>, and <code>j != k</code>, and <code>nums[i] + nums[j] + nums[k] == 0</code>.

Notice that the solution set must not contain duplicate triplets.

**Example 1:** 

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
```

**Example 2:** 

```
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
```

**Example 3:** 

```
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```

**Constraints:** 

- <code>3 <= nums.length <= 3000</code>
- <code>-10^5 <= nums[i] <= 10^5</code>

---

# Solution

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # Sort the array to easily skip duplicates and use two-pointer technique
        nums.sort()
        res = []

        # Loop through each number, treating it as the first number of the triplet
        for i in range(len(nums)):

            # Skip duplicate values for the first element to avoid duplicate triplets
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            # Two pointers for finding the remaining two numbers
            j = i + 1               # left pointer
            k = len(nums) - 1       # right pointer

            # Process until the pointers meet
            while j < k:
                x = nums[i] + nums[j] + nums[k]  # sum of the triplet

                # Sum too large → move right pointer left to reduce value
                if x > 0:
                    k -= 1

                # Sum too small → move left pointer right to increase value
                elif x < 0:
                    j += 1

                else:
                    # Found a valid triplet
                    res.append([nums[i], nums[j], nums[k]])

                    # Move left pointer forward to look for next possible combination
                    j += 1

                    # Skip duplicate values for second element
                    # Ensures no duplicate triplets are recorded
                    while j < k and nums[j] == nums[j - 1]:
                        j += 1
        
        # Return the list of all unique triplets
        return res
```
