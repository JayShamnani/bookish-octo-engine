# [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

Given a string <code>s</code>, find the length of the **longest**  <button type="button" aria-haspopup="dialog" aria-expanded="false" aria-controls="radix-:r1k:" data-state="closed" class="">**substring** </button> without duplicate characters.

**Example 1:** 

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3. Note that <code>"bca"</code> and <code>"cab"</code> are also correct answers.
```

**Example 2:** 

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:** 

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Constraints:** 

- <code>0 <= s.length <= 5 * 10^4</code>
- <code>s</code> consists of English letters, digits, symbols and spaces.

# Solution

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        hmap = dict()
        left = 0
        if not s:
            return 0
        max_length = 0

        for right in range(n):
            if s[right] not in hmap:
                max_length = max(max_length, right - left + 1)
            else:
                if hmap[s[right]] < left:
                    max_length = max(max_length, right - left + 1)
                else:
                    left = hmap[s[right]] + 1
            hmap[s[right]] = right
        return max_length
```
