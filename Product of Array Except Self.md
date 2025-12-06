# [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)

Given an integer array <code>nums</code>, return an array <code>answer</code> such that <code>answer[i]</code> is equal to the product of all the elements of <code>nums</code> except <code>nums[i]</code>.

The product of any prefix or suffix of <code>nums</code> is **guaranteed**  to fit in a **32-bit**  integer.

You must write an algorithm that runs in<code>O(n)</code>time and without using the division operation.

**Example 1:** 

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Example 2:** 

```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

**Constraints:** 

- <code>2 <= nums.length <= 10^5</code>
- <code>-30 <= nums[i] <= 30</code>
- The input is generated such that <code>answer[i]</code> is **guaranteed**  to fit in a **32-bit**  integer.

**Follow up:** Can you solve the problem in <code>O(1)</code>extraspace complexity? (The output array **does not**  count as extra space for space complexity analysis.)


# Solution

## Simple

```py
class Solution:
    def productExceptSelf(self, n: List[int]) -> List[int]:
        # llist[i] = product of all elements to the left of i
        llist = [1] * len(n)

        # rlist[i] = product of all elements to the right of i
        rlist = [1] * len(n)

        # Build prefix product (left side)
        for i in range(1, len(n)):
            llist[i] = n[i - 1] * llist[i - 1]

        # Build suffix product (right side)
        for i in range(len(n) - 2, -1, -1):
            rlist[i] = n[i + 1] * rlist[i + 1]

        # Multiply prefix and suffix for final result
        for i in range(len(n)):
            rlist[i] = rlist[i] * llist[i]

        return rlist
```

## Follow up

```py
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        res = [1] * n
        
        # Step 1: prefix products stored directly in res
        prefix = 1
        for i in range(n):
            res[i] = prefix
            prefix *= nums[i]
        
        # Step 2: multiply with suffix products
        suffix = 1
        for i in range(n - 1, -1, -1):
            res[i] *= suffix
            suffix *= nums[i]
        
        return res
```
