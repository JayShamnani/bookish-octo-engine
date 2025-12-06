# [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)

Given two strings <code>s</code> and <code>p</code>, return an array of all the start indices of <code>p</code>'s <button type="button" aria-haspopup="dialog" aria-expanded="false" aria-controls="radix-:r1k:" data-state="closed" class="">anagrams</button> in <code>s</code>. You may return the answer in **any order** .

**Example 1:** 

```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:** 

```
Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

**Constraints:** 

- <code>1 <= s.length, p.length <= 3 * 10^4</code>
- <code>s</code> and <code>p</code> consist of lowercase English letters.

# Solution

## Brute Force

```py
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        # If both strings are equal, the only anagram starts at index 0
        if p == s:
            return [0]

        phash = Counter(p)     # Count frequencies of pattern string
        w = len(p)             # Sliding window size same as pattern length
        left = 0               # Window start index
        res = list()           # Store starting indices of anagrams

        # Slide over each possible starting point in s
        while left < len(s):
            right = left + w   # Window end index

            # If window exceeds string boundary, no more anagrams possible
            if right > len(s):
                left += 1
                continue

            # Compute freq of substring s[left:right] and compare
            if phash == Counter(s[left:right]):
                res.append(left)

            # Move window by one position
            left += 1

        return res
```

## Sliding Window

```py
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        # If entire strings are equal, the only possible anagram starts at index 0
        if p == s:
            return [0]

        phash = Counter(p)      # Frequency map of characters in pattern p
        w = len(p)              # Size of the sliding window = length of p
        window = Counter()      # Frequency map for current window in s
        res = list()            # Result list to store starting indices of anagrams

        # Iterate over each character index in string s
        for i in range(len(s)):
            window[s[i]] += 1   # Add current character to the window

            # Once window size exceeds w, remove the leftmost character
            if i >= w:
                window[s[i - w]] -= 1
                # Remove the key completely to keep Counter clean (match faster)
                if window[s[i - w]] == 0:
                    del window[s[i - w]]

            # If window matches phash, this is an anagram starting at (i - w + 1)
            if window == phash:
                res.append(i - w + 1)

        return res
```
