# [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/description/)

Given two strings <code>s1</code> and <code>s2</code>, return <code>true</code> if <code>s2</code> contains a <button type="button" aria-haspopup="dialog" aria-expanded="false" aria-controls="radix-:r1k:" data-state="closed" class="">permutation</button> of <code>s1</code>, or <code>false</code> otherwise.

In other words, return <code>true</code> if one of <code>s1</code>'s permutations is the substring of <code>s2</code>.

**Example 1:** 

```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:** 

```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
```

**Constraints:** 

- <code>1 <= s1.length, s2.length <= 10^4</code>
- <code>s1</code> and <code>s2</code> consist of lowercase English letters.

# Solution

```py
class Solution:
    def checkInclusion(self, p: str, s: str) -> bool:
        # If entire strings are equal, the only possible anagram starts at index 0
        if p == s:
            return True

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
                return True

        return False
```
